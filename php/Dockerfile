# Base php image that controls the php version
FROM buildpack-deps:jessie
MAINTAINER Tibor Sári <tiborsari@gmx.de>

ENV DEBIAN_FRONTEND noninteractive

## add dotdeb to apt sources list
RUN echo 'deb http://packages.dotdeb.org jessie all' > /etc/apt/sources.list.d/dotdeb.list
RUN echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list.d/dotdeb.list

## add dotdeb key for apt
RUN curl http://www.dotdeb.org/dotdeb.gpg | apt-key add -

# pin the versions
COPY dotdeb.pin /etc/apt/preferences.d/php

# we need this for the php-fpm pid file
VOLUME /run/php

# update, install and clean up to minimize the image size
RUN \
    apt-get update -qq && \
    apt-get install --no-install-recommends -y \
        locales \
        php-cli \
        sudo \
    && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

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