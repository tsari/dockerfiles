# The composer file has to inherit from the project specific php image, as it needs the same environment.
# php7
FROM tsari/jessie-php-fpm

#php 5.4
#FROM tsari/wheezy-apache-php
MAINTAINER Tibor Sári <tiborsari@gmx.de>

ENV COMPOSER_VERSION 1.4.2

RUN curl -sS --insecure -o /usr/local/bin/composer https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar
RUN chmod +x /usr/local/bin/composer

ADD https://raw.githubusercontent.com/tsari/docker-entrypoint/master/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

# Set up the application directory
VOLUME ["/app"]
WORKDIR /app

# Set up the command arguments
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["composer", "--version"]