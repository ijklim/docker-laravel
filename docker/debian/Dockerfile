ARG BUILD_DEBIAN_VERSION

FROM debian:${BUILD_DEBIAN_VERSION}
MAINTAINER Ivan Lim

RUN apt-get update

# 1. development packages
RUN apt-get install -y apache2 php php-mysql

# 2. apache configs + document root
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR
COPY ./docker/apache/apache.conf /etc/apache2/sites-available/000-default.conf

# 3. mod_rewrite for URL rewrite and mod_headers for .htaccess extra headers like Access-Control-Allow-Origin-
RUN a2enmod rewrite headers

# 4. Start apache
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
