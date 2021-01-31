ARG DOCKER_BUILD_MYSQL_VERSION

FROM mysql:${DOCKER_BUILD_MYSQL_VERSION}
MAINTAINER Ivan Lim

# Available TZ: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
ARG TZ=US/Eastern
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && chown -R mysql:root /var/lib/mysql/

# innodb_use_native_aio setting in my.cnf is important for Windows machine
COPY ./docker/mysql/my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 0444 /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]
