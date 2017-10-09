# Pimcore Docker Test Setup

A simple setup to run Pimcore's test suite in a docker setup. Currently configured for PHP 7.1 and 7.2 through PHP's official
images.

## Prerequisites

* Docker and Docker Compose installed
* PHP and Composer installed as dependencies need to be installed before running tests

## Usage

The setup expects a checkout of the Pimcore repository in `/pimcore`. You can either start with a fresh clone or symlink
an existing installation. `/pimcore` is marked as ignored in `.gitignore` so you can just clone it inside this repository.

```bash
# clone this repository
$ git clone git@github.com:maff/pimcore-docker-test-setup.git

# clone the pimcore repository to /pimcore
$ cd pimcore-docker-test-setup
$ git clone git@github.com:pimcore/pimcore.git

# composer dependencies are not installed when running tests so you need to do it before running tests
$ (cd pimcore && composer install)
```

Now you can run the test suite either on one of the configured PHP images. Currently the following images are available:

* `php7`: latest PHP 7 (7.1 currently)
* `php72`: latest PHP 7.2 RC

```bash
$ docker-compose up -d

# you might need to wait a couple of seconds until DB and Redis are ready
$ docker-compose exec php7 vendor/bin/codecept run -c pimcore

# of course, you can limit the tests to just a single suite or group
$ docker-compose exec php7 vendor/bin/codecept run -c pimcore cache
$ docker-compose exec php7 vendor/bin/codecept run -c pimcore cache -g cache.core.redis
``` 
