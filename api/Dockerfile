FROM ubuntu:bionic
LABEL maintainer="Max Boyar <max.boyar.a@gmail.com>"

ENV API_VERSION=0.0.5

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
RUN mkdir /www && mkdir -p /run/php
ADD https://github.com/meklis/all-ok-radius-nodeny-lib/archive/${API_VERSION}.tar.gz /tmp/lib.tar.gz
RUN tar -zxvf /tmp/lib.tar.gz -C /www --strip-components 1
RUN cd /www && composer update
RUN echo 'catch_workers_output = yes' >> /etc/php/7.2/fpm/pool.d/www.conf

CMD envsubst "$(env | sed -e 's/=.*//' -e 's/^/\$/g')" < \
  /etc/nginx/nginx.conf.template > /etc/nginx/nginx.conf && \
  /usr/bin/supervisord -n -c /etc/supervisord.conf
