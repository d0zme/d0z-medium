---
title: The Importance of Removing Header Details in Web Server Responses
layout: post
permalink: /removing-header-details-web-server-responses
image: https://i.imgur.com/8ao6aaA.jpg
---

By default, web servers return about your installed software & plugins, making your website vulnerable to custom attacks by sopisticated hackers. If you don't keep up with security patches, you are much more open to attacks than you may think. This is why it's important to use some sneaky tactics to remove header details when serving HTML web pages.

## Configuring Unix Servers (Nginx or Apache)

### Content Security Policy

The CSP header allows you to define a white list of approved content sources for your site. By restricting the assets that a browser can load for your site, such as JS and CSS, CSP can act as an effective countermeasure to XSS attacks.

#### Nginx:

<pre>
add_header Content-Security-Policy "default-src https: data: 'unsafe-inline' 'unsafe-eval'" always;
</pre>

#### Apache:

Header always set Content-Security-Policy **"default-src https: data: 'unsafe-inline' 'unsafe-eval'""**

### HTTP Strict Transport Security (HSTS)

HSTS allows you to tell a browser that you always want a user to connect using HTTPS instead of HTTP. This means that any bookmark, link or address will force users to use HTTPS, even if they specify HTTP.

#### NginX:

<pre>
add_header Strict-Transport-Security **"max-age=31536000; includeSubdomains" always;**
</pre>

#### Apache:

Header always set Strict-Transport-Security **"max-age=31536000; includeSubDomains"**

### X-Frame-Options

The X-Frame-Options ( RFC ) header protects visitors against clickjacking attacks. An attacker can load an iFrame on your site and set your website as the source. It's quite easy, for example: <iframe src="https://tudominio.com"></iframe>.

Possible values for the X-Frame-Options header:
- DENY: This setting is the most restrictive and prevents the site's page from being included in an iFrame. This option is optimal if you do not have valid users for an iFrame.
- SAMEORIGIN: If a parent page is for the same domain as the site page, the site page can be included in the iFrame.
- ALLOW-FROM: You can specify a unique URI allowed to frame the site page.

#### NginX:

<pre>
add_header X-Frame-Options "SAMEORIGIN" always;
</pre>

#### Apache:

Header always set X-Frame-Options **"SAMEORIGIN"**

### X-Xss-Protection

This header is used to set up protection against a mirrored XSS. The valid settings for the header are

- 0 disables the protection
- 1 enables protection
- 1; mode=block tells the browser to block the response if it detects an attack instead of disinfecting the script.

####NginX:

<pre>
add_header X-Xss-Protection "1; mode=block" always;
</pre>

#### Apache:

Header always set **X-Xss-Protection "1; mode=block""**

#### X-Content-Type-Options

This header has only one valid value, nosniff. It prevents Google Chrome and Internet Explorer from trying to detect the type of content of a response other than the one the server declares.

#### Nginx:

add_header X-Content-Type-Options **"nosniff" always;**

#### Apache:

Header always set X-Content-Type-Options **"nosniff"**

Let's eliminate some headers

Now let's reduce the amount of information that headers may be disclosing about your server and what is running on it. Servers usually reveal what software is running on them, what versions of the software are there, and what frameworks are being used. Reducing the amount of information you disclose is always very beneficial.

Apache:

There are two directives you need to add, or change in the configuration file /etc/apache/conf.d/security and these are ServerTokens and ServerSignature.

<pre>
ServerSignature Off
ServerTokens Prod
</pre>

The ServerSignature appears at the bottom of Apache-generated pages, for example when displaying error 404 (document not found).

The ServerTokens directive is used to determine what Apache will put in the header of the server's HTTP response.

#### Nginx:

Changing the value of the server header in Nginx is not so easy, but there is a way to do it.

<pre>
server_tokens off;
</pre>

You may also see error messages from the service with some NGINX information. To ensure that this is not reported at any time it is best to modify the following lines in the src/http/ngx_http_special_response.clas file:

<pre>
static u_char ngx_http_error_full_tail[ ] =
"<hr><center>" NGINX_VER "</center>" CRLF
"</body>" CRLF
"</html>" CRLF
;static u_char ngx_http_error_tail[ ] =
"<hr>>center>nginx</center>" CRLF
"</body>" CRLF
"</html>" CRLF
;
</pre>

For others that do not include the variable NGINX_VER:

<pre>
static u_char ngx_http_error_full_tail[ ] = CRLF;
static u_char ngx_http_error_tail[ ] = CRLF;
</pre>
