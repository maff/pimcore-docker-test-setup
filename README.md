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
$ composer install
```

Now you can run the test suite either on one of the configured PHP images. Currently the following images are available:

* `php7`
* `php72`

```bash
$ docker-compose up -d
$ docker-compose exec php7 vendor/bin/codecept run -c pimcore

# of course, you can limit the tests to just a single suite or group
$ docker-compose exec php7 vendor/bin/codecept run -c pimcore cache
$ docker-compose exec php7 vendor/bin/codecept run -c pimcore cache -g cache.core.redis
``` 
