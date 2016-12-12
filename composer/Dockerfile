# The composer file has to inherit from the project specific php image, as it needs the same environment.
FROM tsari/jessie-php-fpm
MAINTAINER Tibor Sári <tiborsari@gmx.de>

ENV COMPOSER_VERSION 1.2.4

RUN curl -S --insecure -o /usr/local/bin/composer https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar
RUN chmod +x /usr/local/bin/composer

# Set up the application directory
VOLUME ["/app"]
WORKDIR /app

CMD ["composer", "--version"]