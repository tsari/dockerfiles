# Base php image that controls the php version
FROM buildpack-deps:jessie
MAINTAINER Tibor Sári <tiborsari@gmx.de>

ENV DEBIAN_FRONTEND noninteractive

RUN \
    apt-get update -qq && \
    apt-get install --no-install-recommends -y \
        apt-transport-https \
        lsb-release \
        ca-certificates \
    && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

## add dotdeb to apt sources list
RUN echo 'deb https://packages.sury.org/php jessie main' > /etc/apt/sources.list.d/php.list
RUN echo 'deb-src https://packages.sury.org/php jessie main' >> /etc/apt/sources.list.d/php.list

## add key for apt
RUN curl https://packages.sury.org/php/apt.gpg | apt-key add -

# pin the versions
COPY php.pin /etc/apt/preferences.d/php

# we need this for the php-fpm pid file
VOLUME /run/php

# update, install and clean up to minimize the image size
RUN \
    apt-get update -qq && \
    apt-get install --no-install-recommends -y \
        locales \
        sudo \
        php7.1-cli \
        php7.1-fpm \
    && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.1/fpm/php.ini

# set locales
RUN echo "de_DE.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8

# Set up the application directory
VOLUME ["/app"]
WORKDIR /app

ADD https://raw.githubusercontent.com/tsari/docker-entrypoint/master/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

# Set up the command arguments
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["php", "-v"]