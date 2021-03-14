FROM alpine:3.13

LABEL maintainer="Sunil Kisoensingh" \
      description="Simple lightweight container including nginx, php, composer & npm based on Alpine Linux"

ENV DEBIAN_FRONTEND noninteractive
ENV TZ="Europe/Amsterdam"

ARG SYSTEMUSERID
ARG SYSTEMUSERNAME
ARG SYSTEMGROUPID
ARG SYSTEMGROUPNAME

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apk update --no-cache && apk upgrade --no-cache && \
    apk --no-cache --update add bash nginx supervisor curl php8 php8-fpm php8-opcache php8-mysqli \
    php8-json php8-openssl php8-curl php8-zlib php8-xml php8-phar php8-intl php8-dom \
    php8-xmlwriter php8-xmlreader php8-fileinfo php8-tokenizer php8-ctype php8-session \
    php8-mbstring php8-gd php8-pdo php8-pdo_mysql

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx/default.conf /etc/nginx/http.d/default.conf

RUN ln -s /usr/bin/php8 /usr/bin/php

RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer && \
    apk --no-cache --update add nodejs nodejs-npm

RUN addgroup -S  $SYSTEMGROUPNAME -g $SYSTEMGROUPID
RUN adduser -u $SYSTEMUSERID -S $SYSTEMUSERNAME -G $SYSTEMGROUPNAME

RUN mkdir -p /var/www/app && \
    mkdir -p /var/log/supervisor && \
    mkdir -p /run/nginx

RUN chown -R $SYSTEMUSERID /var/www/app && \
    chown -R $SYSTEMUSERID /run && \
    chown -R $SYSTEMUSERID /var/lib/nginx && \
    chown -R $SYSTEMUSERID /var/log/nginx && \
    chown -R $SYSTEMUSERID /var/log/supervisor

WORKDIR /var/www/app

COPY runtimes/8.0/php.ini /etc/php8/php.ini
COPY supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY runtimes/8.0/start-container /usr/local/bin/start-container

RUN chmod +x /usr/local/bin/start-container

EXPOSE 8080

ENTRYPOINT ["start-container"]