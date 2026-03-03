# .htaccess Security Rules Reference

## Block Format

All MCM security rules use delimited blocks:
```apache
# BEGIN MCM Security - [measure_id]
[rules]
# END MCM Security - [measure_id]
```

## Rules by Measure

### wpconfig_htaccess_protection
```apache
# BEGIN MCM Security - wpconfig_htaccess_protection
<Files wp-config.php>
    Order allow,deny
    Deny from all
</Files>
# END MCM Security - wpconfig_htaccess_protection
```

### disable_directory_listing
```apache
# BEGIN MCM Security - disable_directory_listing
Options -Indexes
# END MCM Security - disable_directory_listing
```

### uploads_php_execution_block
Place in `wp-content/uploads/.htaccess`:
```apache
# BEGIN MCM Security - uploads_php_execution_block
<Files *.php>
    Deny from all
</Files>
<FilesMatch "\.php$">
    Deny from all
</FilesMatch>
# END MCM Security - uploads_php_execution_block
```

### sensitive_files_protection
```apache
# BEGIN MCM Security - sensitive_files_protection
<FilesMatch "^(wp-config\.php|error_log|debug\.log|readme\.html|license\.txt|.*\.sql|.*\.bak|.*\.backup)$">
    Order allow,deny
    Deny from all
</FilesMatch>
# END MCM Security - sensitive_files_protection
```

### xmlrpc_protection (full_block mode)
```apache
# BEGIN MCM Security - xmlrpc_protection
<Files xmlrpc.php>
    Order allow,deny
    Deny from all
</Files>
# END MCM Security - xmlrpc_protection
```

### hotlinking_protection
```apache
# BEGIN MCM Security - hotlinking_protection
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{HTTP_REFERER} !^$
    RewriteCond %{HTTP_REFERER} !^https://([a-z0-9]+\.)?SITE_DOMAIN [NC]
    RewriteCond %{HTTP_REFERER} !^https://([a-z0-9]+\.)?google\. [NC]
    RewriteCond %{HTTP_REFERER} !^https://([a-z0-9]+\.)?bing\. [NC]
    RewriteRule \.(jpg|jpeg|png|gif|css|js|txt|xml|pdf)$ - [F,L]
</IfModule>
# END MCM Security - hotlinking_protection
```

## Nginx Equivalents

For Nginx servers, provide these rules for manual configuration:

```nginx
# wpconfig_htaccess_protection
location ~* /wp-config\.php$ { deny all; }

# disable_directory_listing
autoindex off;

# uploads_php_execution_block
location ~* /wp-content/uploads/.*\.php$ { deny all; }

# sensitive_files_protection
location ~* \.(sql|bak|backup|log)$ { deny all; }
location = /readme.html { deny all; }
location = /license.txt { deny all; }

# xmlrpc_protection
location = /xmlrpc.php { deny all; }
```
