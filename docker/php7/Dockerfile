FROM php:7-apache

RUN apt-get update \
  && apt-get install -y mysql-client libbz2-dev libicu-dev zlib1g-dev --no-install-recommends \
  && docker-php-ext-install pdo_mysql bz2 intl zip

# setup apache
ENV APACHE_DOCUMENT_ROOT /pimcore/web
RUN a2enmod rewrite actions alias env
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

WORKDIR "/pimcore"
