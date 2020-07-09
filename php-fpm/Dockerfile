FROM alpine:3.11

ADD https://dl.bintray.com/php-alpine/key/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub

RUN apk --update add ca-certificates && \
    echo "https://dl.bintray.com/php-alpine/v3.11/php-7.4" >> /etc/apk/repositories

# install php and some extensions
RUN apk add --update \
    bash \
    curl \
    git \
    zip \
    unzip \
    php \
    php-fpm \
    php-bz2 \
    php-json \
    php-curl \
    php-pdo \
    php-pdo_pgsql \
    php-pdo_mysql \
    php-pdo_sqlite \
    php-redis \
    php-intl \
    php-xsl \
    php-gd \
    php-amqp \
    php-sodium \
    php-ctype \
    php-mbstring \
    php-mongodb \
    php-xml \
    php-xmlreader \
    php-xmlrpc \
    php-xsl \
    php-zip \
    php-zlib \
    php-iconv \
    php-session \
    php-phar \
    php-posix \
    php-opcache \
    php-apcu
    

WORKDIR /var/www

# Add user with uid:gid of 1000:1000 to prevent right access in linux os
ENV USER=docker
ENV UID=1000
ENV GID=1000

RUN addgroup \
    --gid "${GID}" \
    "${USER}"

RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/var/www" \
    --ingroup "$USER" \
    --no-create-home \
    --uid "$UID" \
    "$USER"

RUN ln -s /usr/bin/php7 /usr/bin/php

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install symfony cli
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

CMD ["php-fpm7", "--nodaemonize"]

EXPOSE 9000