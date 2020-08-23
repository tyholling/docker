FROM alpine

RUN apk update \
&&  apk add \
bash \
bc \
curl \
git \
libressl \
netcat-openbsd \
nginx \
openssh \
openssl \
php \
php-fpm \
vim \
wget \
;

RUN passwd -d root \
&&  mkdir -p /run/nginx \
&&  mkdir -p /var/run/sshd \
&&  ssh-keygen -A \
&&  sed -i "s/^\(root:.*\):\/bin\/ash$/\1:\/bin\/bash/" /etc/passwd \
;

RUN git clone https://github.com/tyholling/config.git \
&&  touch config/.toprc \
&&  (cd config; ./install.sh) \
;

RUN adduser -D -g www www \
&&  mkdir -p /www \
&&  chown -R www:www /www \
&&  chown -R www:www /var/lib/nginx \
&&  rm /etc/nginx/conf.d/default.conf \
;

COPY id_rsa.pub /root/.ssh/authorized_keys
COPY nginx.conf /etc/nginx/nginx.conf
COPY startup.sh /tmp/startup.sh
COPY www/ /www/

EXPOSE 22 80 443

CMD [ "/tmp/startup.sh" ]
