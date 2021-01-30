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

  ```


# Installation

* Configure `/docker/.env`

  ```sh
  # Build docker image
  docker-compose --env-file ./docker/.env build --no-cache

  # Start server
  docker-compose --env-file ./docker/.env up

  # Visit website
  http://<docker machine ip>:<APP_PORT_NUMBER specified in /docker/.env>
  ```

* Build docker image `docker-compose --env-file ./docker/.env build`

  * Note: docker-compose v.1.25+ is required to use `--env-file` option

* Start docker application `docker-compose up`


# Resources

* Environment variables in Compose: https://docs.docker.com/compose/environment-variables/