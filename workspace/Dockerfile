FROM php:8.0-fpm

ENV DEBIAN_FRONTEND=noninteractive
ENV LC_ALL=C.UTF-8
ENV LC_CTYPE=C.UTF-8
ENV LANG=C.UTF-8
ENV LANGUAGE=C.UTF-8

ARG APP_NAME=shipping_app

# Install dependencies
RUN apt-get update && apt-get install -qy \
  apt-utils \
  curl \
  fonts-noto \
  fonts-noto-cjk \
  supervisor \
  imagemagick \
  vim \
  sudo

# Install PHP Extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions \
  @composer-1 \
  gd \
  bcmath \
  exif \
  mcrypt \
  pcntl \
  pdo_mysql \
  xmlrpc \
  redis \
  zip \
  imagick

# Add user & group
RUN groupadd -g 1000 app && \
  useradd -u 1000 -g app -G www-data,root -s /bin/bash app

RUN mkdir -p /var/log/app && \
  chown -R www-data:www-data /var/log/app && \
  chmod g+w /var/log/app

USER app
WORKDIR /var/www/html/${APP_NAME}
