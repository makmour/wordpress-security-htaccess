# WordPress Security Rules for .htaccess [![forthebadge](https://forthebadge.com/images/badges/built-by-hipsters.svg)](http://forthebadge.com)

A collection of .htaccess rules which make your WordPress setup more secure without having to use any 3rd party plugin or service.

### Add security headers
``` apacheconf
Header always set X-Xss-Protection "1; mode=block"
Header set X-Content-Type-Options "nosniff"
Header always set X-Frame-Options "DENY"
Header set Strict-Transport-Security "max-age=631138519; includeSubDomains"
Header always set Referrer-Policy "no-referrer-when-downgrade"
```

### Block bruteforcing through xml-rpc
``` apacheconf
RewriteRule ^xmlrpc.php$ "http://0.0.0.0/" [R=301,L]
```
