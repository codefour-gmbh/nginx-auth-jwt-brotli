FROM ubuntu:18.04

RUN apt update && \
    apt upgrade -y && \
    apt install -y apt-transport-https ca-certificates software-properties-common && \
    apt install -y unzip git tree curl && \
    apt install -y build-essential dpkg-dev zlib1g-dev libpcre3 libpcre3-dev libjwt0 libjwt-dev libjansson4 libjansson-dev && \
    curl -L https://nginx.org/keys/nginx_signing.key | apt-key add - && \
    echo "deb http://nginx.org/packages/ubuntu/ bionic nginx" > /etc/apt/sources.list.d/nginx.list && \
    echo "deb-src http://nginx.org/packages/ubuntu/ bionic nginx" >> /etc/apt/sources.list.d/nginx.list && \
    apt-get update && \
    cd /usr/local/src && \
    apt source nginx && \
    apt build-dep nginx -y && \
    git clone --recursive https://github.com/google/ngx_brotli.git && \
    git clone --recursive https://github.com/r-chris/ngx_http_auth_jwt_module.git && \
    cd /usr/local/src/nginx-*
    sed -i 's$ --group=nginx $ --group=nginx --add-module=/usr/local/src/ngx_brotli --add-module=/usr/local/src/ngx_http_auth_jwt_module $g' debian/rules
    dpkg-buildpackage -b -uc -us && \
    cd /usr/local/src/ && \
    dpkg -i nginx_*.deb && \
    cd /etc/nginx/
