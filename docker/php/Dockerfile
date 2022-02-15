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

RUN apk --no-cache update \
  && apk --no-cache upgrade \
  && apk --no-cache add \
  oniguruma-dev \
  curl-dev \
  freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev \
  libzip-dev \
  libxml2-dev \
  pcre-dev \
  && docker-php-source extract \
  && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
  && docker-php-ext-configure zip \
  && docker-php-ext-install -j$(nproc) mbstring curl xml zip pdo pdo_mysql mysqli gd iconv pcntl sysvshm sysvsem sysvmsg shmop opcache redis

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /workspace