# Ngnix Web Template for Hestia Control Panel

1. cd /usr/local/hestia/data/templates/web/nginx/
2. cp default.tpl websitename.tpl
3. cp default.stpl websitename.stpl
4. nano website.tpl
5. And replace:
https://github.com/hestiacp/hestiacp/blob/e329bd2167e29d3cf92f2b0cfed7bdfb7582ddb6/install/deb/templates/web/nginx/default.tpl#L14-L21
With:
proxy_pass      http://%ip%:8086;
Note: Replace 8086 by port number of http port number
6. Remove:
        location ~ ^.+.(%proxy_extensions%)$ {
            root           %sdocroot%;
            access_log     /var/log/%web_system%/domains/%domain%.log combined;
            access_log     /var/log/%web_system%/domains/%domain%.bytes bytes;
            expires        max;
            try_files      $uri @fallback;
        }

Example : 

#=========================================================================#
# Default Web Domain Template                                             #
# DO NOT MODIFY THIS FILE! CHANGES WILL BE LOST WHEN REBUILDING DOMAINS   #
# https://docs.hestiacp.com/admin_docs/web.html#how-do-web-templates-work #
#=========================================================================#

server {
    listen      %ip%:%proxy_ssl_port% ssl http2;
    server_name %domain_idn% %alias_idn%;
    ssl_certificate      %ssl_pem%;
    ssl_certificate_key  %ssl_key%;
    ssl_stapling on;
    ssl_stapling_verify on;
    error_log  /var/log/%web_system%/domains/%domain%.error.log error;

    include %home%/%user%/conf/web/%domain%/nginx.hsts.conf;

    location / {
        proxy_pass      http://%ip%:8096;
    }

    location /error/ {
        alias   %home%/%user%/web/%domain%/document_errors/;
    }

    location @fallback {
        proxy_pass      http://%ip%:%web_ssl_port%;
    }

    location ~ /.(?!well-known/|file) {
       deny all;
       return 404;
    }                                                                                                                                                                                                                                          proxy_hideheader Upgrade;

    include %home%/%user%/conf/web/%domain%/nginx.ssl.conf;
}

Note: Replace 8096 by the port number of the http port number

7. nano website.stpl

8. And replace:
https://github.com/hestiacp/hestiacp/blob/e329bd2167e29d3cf92f2b0cfed7bdfb7582ddb6/install/deb/templates/web/nginx/default.tpl#L14-L21
With:
proxy_pass      http://%ip%:8086;
Note: Replace 8086 by port number of https port number

9. Remove:
        location ~ ^.+.(%proxy_extensions%)$ {
            root           %sdocroot%;
            access_log     /var/log/%web_system%/domains/%domain%.log combined;
            access_log     /var/log/%web_system%/domains/%domain%.bytes bytes;
            expires        max;
            try_files      $uri @fallback;
        }

Example : 

#=========================================================================#
# Default Web Domain Template                                             #
# DO NOT MODIFY THIS FILE! CHANGES WILL BE LOST WHEN REBUILDING DOMAINS   #
# https://docs.hestiacp.com/admin_docs/web.html#how-do-web-templates-work #
#=========================================================================#

server {
    listen      %ip%:%proxy_ssl_port% ssl http2;
    server_name %domain_idn% %alias_idn%;
    ssl_certificate      %ssl_pem%;
    ssl_certificate_key  %ssl_key%;
    ssl_stapling on;
    ssl_stapling_verify on;
    error_log  /var/log/%web_system%/domains/%domain%.error.log error;

    include %home%/%user%/conf/web/%domain%/nginx.hsts.conf;

    location / {
        proxy_pass      http://%ip%:8096;
    }

    location /error/ {
        alias   %home%/%user%/web/%domain%/document_errors/;
    }

    location @fallback {
        proxy_pass      http://%ip%:%web_ssl_port%;
    }

    location ~ /.(?!well-known/|file) {
       deny all;
       return 404;
    }                                                                                                                                                                                                                                          proxy_hideheader Upgrade;

    include %home%/%user%/conf/web/%domain%/nginx.ssl.conf;
}

Note: Replace 8096 by the port number of the https port number

10. Go to hestia control panel

11. Go the domain

12. Click on Edit

13. Click on Advanced Options

14. Under Proxy Template select the template you just created.

15. Click Save
