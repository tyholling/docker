FROM alpine

RUN apk update \
&&  apk upgrade \
&&  apk add --no-cache \
bash \
bc \
composer \
curl \
git \
libressl \
netcat-openbsd \
nginx \
openssh \
openssl \
php7 \
php7-apcu \
php7-bcmath \
php7-bz2 \
php7-ctype \
php7-curl \
php7-dom \
php7-fpm \
php7-gd \
php7-gettext \
php7-gmp \
php7-iconv \
php7-json \
php7-mbstring \
php7-mcrypt \
php7-mysqli \
php7-odbc \
php7-openssl \
php7-pdo \
php7-pdo_dblib \
php7-pdo_mysql \
php7-pdo_odbc \
php7-pdo_pgsql \
php7-pdo_sqlite \
php7-phar \
php7-soap \
php7-sqlite3 \
php7-xml \
php7-xmlreader \
php7-xmlrpc \
php7-zip \
vim \
wget \
;

RUN passwd -d root \
&&  mkdir -p /run/nginx \
&&  mkdir -p /var/run/sshd \
&&  ssh-keygen -A \
&&  sed -i "s/^\(root:.*\):\/bin\/ash$/\1:\/bin\/bash/" /etc/passwd \
\
&&  openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt \
    -subj "/C=US/ST=/L=/O=/OU=/CN=" \
&&  openssl dhparam -out /etc/nginx/dhparam.pem 4096 \
\
&&  adduser -D -g www www \
&&  mkdir -p /www \
&&  chown -R www:www /www \
&&  chown -R www:www /var/lib/nginx \
&&  composer require aws/aws-sdk-php-symfony \
\
&&  git clone https://github.com/tyholling/config.git /tmp/config \
&&  touch /tmp/config/.toprc \
&&  (cd /tmp/config; ./install.sh) \
&&  git clone https://github.com/Neilpang/acme.sh.git /tmp/acme \
&&  (cd /tmp/acme; ./acme.sh --install) \
;

COPY entrypoint.sh /entrypoint.sh
COPY id_rsa.pub /root/.ssh/authorized_keys
COPY nginx.conf /etc/nginx/nginx.conf
COPY www/ /www/

EXPOSE 22 80 443

ENTRYPOINT [ "/entrypoint.sh" ]
