---
title: A simple way to backup Linux servers with the help of FTP
layout: post
image: https://upload.wikimedia.org/wikipedia/commons/thumb/3/36/1st-ftp-southpole-1994.jpg/1024px-1st-ftp-southpole-1994.jpg
---

The are a lot of topics about how useful backups are. Below you can see examples of simple scripts to backup files and MySQL databases with the follow up uploading to the FTP server.

Inventory
Virtual and physical server with Linux OS, web server and MySQL databases

Web server files' are located in the following folders:

/home/site1

/home/site2

/home/site3

The task
To create a script for handy daily backups of files and databases with the follow up saving to FTP.

Solution
To simplify, we will work under the root, with the /root/backup/server, and the place for dumps /root/backup/mysql

Backup for files
Below you can see a script to make a backup for files:

#!/bin/sh
### System Setup ###
BACKUP=/root/backup/server

### FTP ###
FTPD="/"
FTPU="username" [login of the remote FTP]
FTPP="megapassword" [password for the FTP]
FTPS="my_remote_backup.ru" [FTP address]

### Binaries ###
TAR="$(which tar)"
GZIP="$(which gzip)"
FTP="$(which ftp)"

## Today + hour in 24h format ###
NOW=$(date +%Y%m%d) [current data and time to have the file with the name-YYYYMMDD.tar.gz]

### Create tmp dir ###

mkdir $BACKUP/$NOW
$TAR -cf $BACKUP/$NOW/etc.tar /etc [to simplify will copy it all]
$TAR -cf $BACKUP/$NOW/site1.tar /home/site1/
$TAR -cf $BACKUP/$NOW/site2.tar /home/site2/
$TAR -cf $BACKUP/$NOW/site2.tar /home/site3/

ARCHIVE=$BACKUP/server-$NOW.tar.gz
ARCHIVED=$BACKUP/$NOW

$TAR -zcvf $ARCHIVE $ARCHIVED

### ftp ###
cd $BACKUP
DUMPFILE=server-$NOW.tar.gz
$FTP -n $FTPS <<END_SCRIPT
quote USER $FTPU
quote PASS $FTPP
cd $FTPD
mput $DUMPFILE
quit
END_SCRIPT

### clear ###

rm -rf $ARCHIVED
The output of the script above will be a file in the /root/backup/server folder with the YYYYMMDD.tar.gz name. It will contain tar-acrhives in the etc, /home/site1, /home/site2 and /home/site3 archives. This file will be uploaded to the FTP server, which was indicated at the beginning of the script.

MySQL backup
By this script we upload MySQL databases (make dump). Each database is uploaded in a separate file.

#!/bin/sh
# System + MySQL backup script
### System Setup ###
BACKUP=/root/backup/mysql

### Mysql ### [access to our MySQL database]
MUSER="root"
MPASS="megapassword"
MHOST="localhost"

### FTP ###
FTPD="/"
FTPU="username" [login]
FTPP="megapassword" [password]
FTPS="my_remote_backup.ru" [FTP address]

### Binaries ###
TAR="$(which tar)"
GZIP="$(which gzip)"
FTP="$(which ftp)"
MYSQL="$(which mysql)"
MYSQLDUMP="$(which mysqldump)"

## Today + hour in 24h format ###
NOW=$(date +%Y%m%d)

### Create temp dir ###

mkdir $BACKUP/$NOW

### name Mysql ###
DBS="$($MYSQL -u $MUSER -h $MHOST -p$MPASS -Bse 'show databases')"
for db in $DBS
do

### ###
mkdir $BACKUP/$NOW/$db
FILE=$BACKUP/$NOW/$db/$db.sql.gz
echo $i; $MYSQLDUMP --add-drop-table --allow-keywords -q -c -u $MUSER -h $MHOST -p$MPASS $db $i | $GZIP -9 > $FILE
done

ARCHIVE=$BACKUP/mysql-$NOW.tar.gz
ARCHIVED=$BACKUP/$NOW

$TAR -zcvf $ARCHIVE $ARCHIVED

### ftp ###
cd $BACKUP
DUMPFILE=mysql-$NOW.tar.gz
$FTP -n $FTPS <<END_SCRIPT
quote USER $FTPU
quote PASS $FTPP
cd $FTPD
mput $DUMPFILE
quit
END_SCRIPT

### clear ###

rm -rf $ARCHIVED

The output of the script above will be a file in the /root/backup/server folder with the mysql-YYYYMMDD.tar.gz name. It will contain tar-acrhives with all databases dumps. This file will be uploaded to the FTP server, which was indicated at the beginning of the script.

Automatisation
Save this scripts in the /etc/cron.daily folder. But before that check the file /etc/crontab in order to be sure that daily backups are run from this folder.

Conclusion
Of course, in each case the script could be somehow different. Above you can see one of the ways to do that.
