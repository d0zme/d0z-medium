---
title: 3 interesting features of MySQL I bet you didn't know about
layout: post
image: https://upload.wikimedia.org/wikipedia/commons/4/41/Screenshot-mysql-client-text-debian.png
---

While doing the exploration of MySQL source code, I found out some interesting features. Let's take a look on them.

## ENUM

First of all, we will talk about ENUM data type.

<pre>
mysql> CREATE TABLE enums(a ENUM('c', 'a', 'b'), b INT, KEY(a));
Query OK, 0 rows affected (0.36 sec)
mysql> INSERT INTO enums VALUES('a', 1), ('b', 1), ('c', 1);
Query OK, 3 rows affected (0.05 sec)
Records: 3  Duplicates: 0  Warnings: 0
Well, we have a table consisting of two columns. First column, column a, has ENUM type. The second, column b, has INT type. Also this table consists of three rows. All rows in the column b, have a value of 1. What values have the minimum and the maximum elements of the column a?

mysql> SELECT MIN(a), MAX(a) FROM enums;
+--------+--------+
| MIN(a) | MAX(a) |
+--------+--------+
| c      | b      |
+--------+--------+
1 row in set (0.00 sec)
</pre>

It seems strange. I suppose it would be more reasonable if the minimum was a and the maximum was c. So, what if we ask to choose minimum and maximum among such a rows where b is 1?

<pre>
mysql> SELECT MIN(a), MAX(a) FROM enums WHERE b = 1;
+--------+--------+
| MIN(a) | MAX(a) |
+--------+--------+
| a      | c      |
+--------+--------+
1 row in set (0.00 sec)

</pre>

That is how we made MySQL change its mind about the comparing of ENUM fields only by adding a predicate. Why did this happen? Because in case of the first situation MySQL uses index and in the second situation it doesn't use index.

The second example is even shorter:

<pre>
mysql> (SELECT * FROM moo LIMIT 1) LIMIT 2;
+------+
| a    |
+------+
|    1 |
|    2 |
+------+
2 rows in set (0.00 sec)
</pre>

When I showed this query to my colleague, who is in charge of SQL parser, he asked me not “Why this query returns two lines?" but “How to write SQL parser to make this query valid without the special rule which allows such a query?"

It is interesting that not every SELECT framed by round brackets will work properly. For example, UNION framed by round brackets is a syntax error:

<pre>
mysql> (SELECT * FROM moo UNION ALL SELECT * FROM hru) LIMIT 2;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'UNION ALL SELECT * FROM hru) LIMIT 2' at line 1
Here are some more interesting examples of strange behavior.
</pre>

## UNION and LIMIT

<pre>
mysql> 
    -> SELECT 1 FROM moo LIMIT 1
    ->     UNION ALL
    -> SELECT 1 FROM hru LIMIT 1;
+---+
| 1 |
+---+
| 1 |
+---+
1 row in set (0.00 sec)
</pre>

Although both tables are not empty, only one line returned. It happened because the second LIMIT belongs not only to the right part of UNION but to the whole query.

Here we should say some words about shift-reduce conflict. Modern databases with open source have parser written by bison. This parser is called L1-parser. It means that parser should understand the destination of the current token without looking at more than one following token.

For example, in the query above parser cannot understand if LIMIT belongs to the second query or to the whole UNION. If parser cannot understand the meaning of query only by the following query, the situation is called shift-reduce conflict. In this case parser would choose solution according to the set of rules. Unfortunately, such an approach leads to the errors while running adequate query.

So, what if I want to refer LIMIT to the second SELECT and to the UNION?

<pre>
mysql>   SELECT 1 FROM moo
    ->       UNION ALL
    ->   SELECT 1 FROM hru LIMIT 1
    -> LIMIT 2;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'LIMIT 2' at line 4
</pre>

It is impossible because of shift-reduce conflict. Taking the first LIMIT parser cannot see the second LIMIT. That's why parser assumes that the first LIMIT refers to the whole query not to the first part of it.

PostgreSQL does not have shift-reduce conflict at all. Moreover, only UNION can have LIMITs, SELECT cannot have them.

MySQL has more than 160 of such conflicts.

One of the clearest examples of such conflict is joins. It is known that MySQL supports CROSS JOINs and INNER JOINs. The first ones do not have predicates, the second ones have predicates. CROSS JOIN and INNER JOIN are different but they are synonyms in MySQL. It means that INNER JOIN may have no predicate and CROSS JOIN may have some predicate. It can lead to some interesting error:

<pre>
mysql> SELECT * FROM     
    ->     moo
    ->     INNER JOIN
    ->        hru
    ->        INNER JOIN
    ->        baa
    ->        ON hru.a = baa.a
    ->     ON moo.a = hru.a
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'ON moo.a = hru.a' at line 8
</pre>

When parser accept first ON, it does not know about the second and has to decide is it ON for hru and baa or is it ON fro moo and for result of hru and baa connection. In case of the second situation hru and baa are connected without predicate. If we replace INNER JOIN by LEFT JOIN which cannot work without predicate, we will get the following proper working query:

<pre>
mysql> SELECT * FROM     
    ->     moo
    ->     LEFT JOIN
    ->        hru
    ->        LEFT JOIN
    ->        baa
    ->        ON hru.a = baa.a
    ->     ON moo.a = hru.a
    -> ;
+------+------+------+------+
| a    | a    | b    | a    |
+------+------+------+------+
|    1 |    1 | 1    |    1 |
|    2 |    2 | 2    |    2 |
+------+------+------+------+
2 rows in set (0.00 sec)
</pre>

The most interesting fact is that if you want to compile the code with shift-reduce conflict, you have to write the number of such conflicts right in the Bison code. It means that once one of programmers of MySQL made CROSS JOIN and INNER JOIN synonyms, tried to run the code, failed. Also, he got the message that parse is not able to deparse some particular queries. So, he made a decision to correct code and enlarged the number of possible errors.

However, if we speak about some strange moments of MySQL, let's remember this story.

Here one programmer made letter “s" equal the letter “ß" for utf8 in collation. It has any sense only for German language but still not for all situations. And this solution became a great issue as different lines may become equal.

This changing was not only useful but harmful, too. I made the process of movement from 5.0 to 5.1 very hard for utf8 databases with German lines. It happened so because unique indexes got repetitive elements.

## Collations

There is another interesting example with collations.

We have table of three rows with collations:

<pre>
CREATE TABLE strings(
    swedish VARCHAR(100) COLLATE utf8_swedish_ci,
    spanish VARCHAR(100) COLLATE utf8_spanish_ci,
    bin VARCHAR(100) COLLATE utf8_bin
);
</pre>

Run the following query:

<pre>
mysql> SELECT * FROM strings WHERE swedish > bin AND swedish < spanish;
ERROR 1267 (HY000): Illegal mix of collations (utf8_swedish_ci,IMPLICIT) and (utf8_spanish_ci,IMPLICIT) for operation '<'
MySQL reports that it is impossible to compare Swedish and Spanish.
</pre>

Let's write equal query:

<pre>
mysql> SELECT * FROM strings WHERE swedish BETWEEN bin AND spanish;
 Empty set (0.00 sec)
In this case our query became valid although it still compares Swedish and Spanish.
</pre>

Now I want to compare lines vice versa, Spanish with Swedish:

<pre>
mysql> SELECT * FROM strings WHERE swedish BETWEEN spanish AND bin;
ERROR 1270 (HY000): Illegal mix of collations (utf8_swedish_ci,IMPLICIT), (utf8_spanish_ci,IMPLICIT), (utf8_bin,IMPLICIT) for operation 'between'
It is restricted.
</pre>

MySQL has rather strange realize of BETWEEN. If the first or the second parameter has binary collation, all lines will be compared as binary and collation will be ignored. But if the third argument has the binary collation, this logic does not work.

I want to end this talk about strange behavior of MySQL functions with one beautiful example:

<pre>
mysql> SELECT LEAST(9, 11);
+--------------+
| LEAST(9, 11) |
+--------------+
|            9 |
+--------------+
1 row in set (0.00 sec)
</pre>

Here are no surprises.

<pre>
mysql> SELECT LEAST("9", "11");
 +------------------+ 
| LEAST("9", "11") | 
+------------------+ 
| 11 | 
+------------------+
1 row in set (0.00 sec)
</pre>

It seems reasonable, too. Line 11 is smaller than line 9.

What if we add line 11 to line 11?

<pre>
mysql> SELECT LEAST("9", "11") + LEAST("9", "11");
+-------------------------------------+
| LEAST("9", "11") + LEAST("9", "11") |
+-------------------------------------+
|                                  18 |
+-------------------------------------+
1 row in set (0.00 sec)
</pre>

Certainly, we would have 18. It means that function returns different meaning depending on the context. Can we make LAST return three different values depending on the context? We can:
<pre>
mysql> SELECT LEAST("9e1", "110");
+---------------------+
| LEAST("9e1", "110") |
+---------------------+
| 110                 |
+---------------------+
1 row in set (0.00 sec)
mysql> SELECT LEAST("9e1", "110") + 0;
+-------------------------+
| LEAST("9e1", "110") + 0 |
+-------------------------+
|                      90 |
+-------------------------+
1 row in set (0.00 sec)
mysql> SELECT LEAST("9e1", "110") & -1;
+--------------------------+
| LEAST("9e1", "110") & -1 |
+--------------------------+
|                        9 |
+--------------------------+
1 row in set, 1 warning (0.00 sec)
mysql> SHOW WARNINGS;
+---------+------+------------------------------------------+
| Level   | Code | Message                                  |
+---------+------+------------------------------------------+
| Warning | 1292 | Truncated incorrect INTEGER value: '9e1' |
+---------+------+------------------------------------------+
1 row in set (0.00 sec)
</pre>

However, we should mention accepting one warning.

In order to surprise yourself even more, we should meet function NULLIF. It accepts two arguments and returns NULL if arguments are the same or the value of the first argument if they differs. We will not wonder why such a function exists but look at it:

<pre>
mysql> SELECT NULLIF(LEAST("9", "11"), "11") + 0;
+------------------------------------+
| NULLIF(LEAST("9", "11"), "11") + 0 |
+------------------------------------+
|                               NULL |
+------------------------------------+
1 row in set (0.00 sec)
mysql> SELECT NULLIF(LEAST("9", "11"), "12") + 0;
+------------------------------------+
| NULLIF(LEAST("9", "11"), "12") + 0 |
+------------------------------------+
|                                  9 |
+------------------------------------+
1 row in set (0.00 sec)
</pre>

In the first case we got NULL. It means that LEAST really returned line 11. The second query contained the same syntax, arguments of the same type, but NULL had the other constant. We got the value 9. So, despite having the same parameters LEAST returned 11after the first query and 9 after the second.

We can do even better:
<pre>
mysql> SELECT NULLIF(LEAST("9", "11"), "9") + 0;
+-----------------------------------+
| NULLIF(LEAST("9", "11"), "9") + 0 |
+-----------------------------------+
|                                 9 |
+-----------------------------------+
1 row in set (0.00 sec)
</pre>

After this query LEAST returned not line 9 (if it returned 9, NULLIF returned NULL) and in the same time it returned line 9. So, LEAST was run two times. The first time it compared parameters as lines, the second time - as whole numbers.
