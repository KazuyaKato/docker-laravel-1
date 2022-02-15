FROM php:8.1-fpm-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

RUN apk --no-cache update \
  && apk --no-cache upgrade \
  && apk --no-cache add \
  bash \
  shadow \
  tzdata \
  git \
  curl \
  nodejs npm yarn \
  openssl \
  && cp /usr/share/zoneinfo/Japan /etc/localtime

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /workspace