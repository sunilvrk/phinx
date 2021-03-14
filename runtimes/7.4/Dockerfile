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
    apk --no-cache --update add bash nginx supervisor curl php7 php7-fpm php7-opcache php7-mysqli \
    php7-json php7-openssl php7-curl php7-zlib php7-xml php7-phar php7-intl php7-dom \
    php7-xmlwriter php7-xmlreader php7-fileinfo php7-tokenizer php7-ctype php7-session \
    php7-mbstring php7-gd php7-pdo php7-pdo_mysql

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx/default.conf /etc/nginx/http.d/default.conf

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

COPY runtimes/7.4/php.ini /etc/php7.4/php.ini
COPY runtimes/7.4/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY runtimes/7.4/start-container /usr/local/bin/start-container

RUN chmod +x /usr/local/bin/start-container

EXPOSE 8080

ENTRYPOINT ["start-container"]