FROM php:7.4.11-fpm


# Download script to install PHP extensions and dependencies
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
      curl \
      git \
      zip unzip \
    && install-php-extensions \
      bcmath \
      bz2 \
      calendar \
      exif \
      gd \
      intl \
      ldap \
      memcached \
      mysqli \
      opcache \
      pdo_mysql \
      pdo_pgsql \
      pgsql \
      redis \
      soap \
      xsl \
      zip \
      sockets \
      pdo_sqlsrv \
      sqlsrv \
      xdebug
# already installed:
#      iconv \
#      mbstring \

RUN curl -sS https://getcomposer.org/download/2.0.0/composer.phar --output /usr/bin/composer
RUN chmod +x /usr/bin/composer

RUN groupadd -g 1000 magento
RUN mkdir -p /home/magento
RUN useradd -d /home/magento -s /bin/bash -u 1000 -g 1000 magento
RUN chown magento:magento /home/magento
RUN mkdir -p /var/www/html
RUN chown -R magento:magento /var/www

WORKDIR /var/www/html
RUN chown magento:magento /usr/bin/composer