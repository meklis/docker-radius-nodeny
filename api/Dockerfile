FROM ubuntu:bionic
LABEL maintainer="Max Boyar <max.boyar.a@gmail.com>"

ENV TZ=Europe/Kiev
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt update && \
    apt -y upgrade && \
    apt -y install \
    git \
    nginx \
    php-fpm \
    php-json \
    php-mysql \
    php-mbstring \
    php-zip \
    php-yaml \
    php-pdo \
    composer \
    supervisor \
    gettext

COPY nginx.conf /etc/nginx/nginx.conf.template
COPY supervisord.conf /etc/supervisord.conf
RUN mkdir /wwww && mkdir -p /run/php
ADD https://github.com/meklis/all-ok-radius-nodeny-lib/archive/0.0.1-a.tar.gz /www

CMD envsubst "$(env | sed -e 's/=.*//' -e 's/^/\$/g')" < \
  /etc/nginx/nginx.conf.template > /etc/nginx/nginx.conf && \
  /usr/bin/supervisord -n -c /etc/supervisord.conf
