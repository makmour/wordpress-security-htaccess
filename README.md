# WordPress Security Rules for .htaccess [![forthebadge](https://forthebadge.com/images/badges/built-by-hipsters.svg)](http://forthebadge.com)

A collection of .htaccess rules which make your WordPress setup more secure without having to use any 3rd party plugin or service.

**Disclaimer**: While dropping the snippet into an `.htaccess` file is most of the time sufficient, there are cases when certain modifications might be required. Editing your .htaccess may alos bring your site(s) offline so make sure to create a backup of your original .htaccess prior modifying it.

## Add security headers
``` apacheconf
Header always set X-Xss-Protection "1; mode=block"
Header set X-Content-Type-Options "nosniff"
Header always set X-Frame-Options "DENY"
Header set Strict-Transport-Security "max-age=631138519; includeSubDomains"
Header always set Referrer-Policy "no-referrer-when-downgrade"
```

## Disable directory browsing
``` apacheconf
Options All -Indexes
```

## Block bruteforcing through xml-rpc
``` apacheconf
RewriteRule ^xmlrpc.php$ "http://0.0.0.0/" [R=301,L]
```

## Deny public access to .htaccess, wp-config.php and readme.html
``` apacheconf
<FilesMatch "(.htaccess|wp-config.php|readme.html)">
order allow,deny
deny from all
</files>
```

## Deny spam comments from visitors with no referrer
``` apacheconf
RewriteCond %{REQUEST_METHOD} POST
RewriteCond %{REQUEST_URI} .wp-comments-post\.php*
RewriteCond %{HTTP_REFERER} !.*YOURDOMAIN.com.* [OR]
RewriteCond %{HTTP_USER_AGENT} ^$
RewriteRule (.*) ^http://%{REMOTE_ADDR}/$ [R=301,L]
```

## block user enumeration
``` apacheconf
RewriteCond %{QUERY_STRING} (^|&)author=
RewriteRule . http://%{SERVER_NAME}/? [L]
```

Curators
========
[Makis Mourelatos](https://www.linkedin.com/in/makismour/)
