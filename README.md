# Building Laravel with Docker

# Requirements

* Composer

# How project is created

  ```sh
  # Create Laravel 8.25.0 project in folder `docker-laravel`
  composer create-project laravel/laravel docker-laravel

  # Enter newly created folder
  cd docker-laravel
  mkdir docker

  # Create docker related files
  # docker-compose.yml at root
  # Configuration files in `/docker`
  # Minimal setup requires:
  #   • /docker/apache/apache.conf
  #   • /docker/debian/Dockerfile
  #   • /docker/php/php.ini
  # Add docker environment variables to `/.env` file

  ```


# Installation

* Copy database backup `.sql` script to folder `/docker/mysql/docker-entrypoint-initdb.d`

* Copy `/.env.example` to `/.env`, make configuration changes to section below `Docker Setup` if necessary

  * Copy command `cp .env.example .env`

  * Likely candidates for modifications:

    * DB_HOST, DB_DATABASE, DB_USERNAME, DB_PASSWORD

    * DOCKER_WEB_CONTAINER_NAME, DOCKER_WEB_PORT_NUMBER

    * DOCKER_DB_CONTAINER_NAME

    * DOCKER_BUILD_DEBIAN_VERSION

    * DOCKER_BUILD_MYSQL_VERSION

* Docker commands

  ```sh
  # On Windows, make sure to launch Docker Quickstart Terminal
  # Build docker image
  docker-compose build
  # Use `docker-compose build --no-cache` to rebuild from scratch
  # Use `docker-compose build --no-cache web` to rebuild from scratch a specifi service
  # To check instructions with added environment variables `docker-compose config`

  # Start server
  docker-compose up

  # Visit website
  http://<docker machine ip>:<DOCKER_WEB_PORT_NUMBER specified in /docker/.env>

  # To troubleshoot: Attach bash terminal to web
  docker exec -ti <DOCKER_WEB_CONTAINER_NAME> bash
  # cd /var/www/html to run artisan commands

  # To troubleshoot: Attach bash terminal to MySQL
  docker exec -ti <DOCKER_DB_CONTAINER_NAME> bash

  # Stop server
  docker-compose down
  ```


# Resources

* Environment variables in Compose: https://docs.docker.com/compose/environment-variables/

* MySQL docker configurations: https://hub.docker.com/_/mysql


# Notes

* MySQL databases are store in `/var/lib/mysql/`, connect to the db container to find this folder

* If using Ubuntu instead of Debian, change all instances of 'debian' to 'ubuntu' in `docker-compose.yml` (keeping case)

* Check `phpinfo()` for `Loaded Configuration File`, the `/usr/local/etc/php/php.ini` volume mapping in `docker-compose.yml` might need to be changed accordingly