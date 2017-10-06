FROM php:7.2-rc-cli

RUN apt-get update \
  && apt-get install -y mysql-client libbz2-dev libicu-dev zlib1g-dev --no-install-recommends \
  && docker-php-ext-install pdo_mysql bz2 intl zip

WORKDIR "/pimcore"
