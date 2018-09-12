# make your own nginx
- based on regular nginx based on ubuntu 18.04 LTS
- https://www.howtoforge.com/tutorial/how-to-install-nginx-with-brotli-compression-on-ubuntu-1804/

# added modules
- brotli compression (https://github.com/google/ngx_brotli)
- TODO: consider switching this to: https://github.com/eustas/ngx_brotli
- auth jwt Option1: (https://github.com/r-chris/ngx_http_auth_jwt_module)
  - very close to the NGINX pro version in terms of config
  - we had problems getting this one working
- auth jwt Option2: (https://github.com/r-chris/nginx-jwt-module)
  - looks slim and well done (trying this one now)
- auth jwt Option3: (https://github.com/r-chris/ngx-http-auth-jwt-module)
  - in it's current form it comes with auto-redirect (to a login page)
  - fork with "simplification" PR: https://github.com/maxx-t/ngx-http-auth-jwt-module
  - the fork actually removes that and suggests to just use nginx error_codes for that
- auth jwt Option4: (https://github.com/ch1bo/nginx-jwt)
  - no documentation

# the manual nginx compile way
```
wget https://nginx.org/download/nginx-1.15.3.tar.gz
tar zxvf nginx-1.15.3.tar.gz nginx-1.15.3/
cd ~/nginx-1.15.3/
./configure
make
```

# the ubuntu based nginx compile way
```
cd /usr/local/src/nginx-*/
vim debian/rules
```

# added extensions
```
--add-module=/usr/local/src/ngx_brotli
--add-module=/usr/local/src/ngx_http_auth_jwt_module
```

# enable nginx brotli
```
cd /etc/nginx/
vim nginx.conf
...
    brotli on;
    brotli_comp_level 6;
    brotli_static on;
    brotli_types text/plain text/css application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript image/x-icon image/vnd.microsoft.icon image/bmp image/svg+xml;
```

maybe move this into: `include /etc/nginx/conf.d/*.conf;`
