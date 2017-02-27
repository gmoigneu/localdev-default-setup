FROM php:7.0-fpm

# Environements
ENV GOSU_VERSION 1.7
ENV DOCKERIZE_VERSION 0.2.0

# Dependencies
RUN apt-get update \
    && apt-get install -y \
        libpq-dev \
        libicu-dev \
        zlib1g-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libmcrypt4 \
        libmcrypt-dev \
        libcurl4-openssl-dev \
        libxml2-dev \
        curl \
        vim \
        git \
        wget \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install opcache curl mbstring dom mcrypt intl pdo_mysql zip gd exif \
    && pecl install xdebug \
    && pecl install apc \
    && curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/local/bin \
    && php -r "readfile('https://s3.amazonaws.com/files.drush.org/drush.phar');" > drush && mv drush /usr/local/bin && chmod +x /usr/local/bin/drush \
    && curl -sS https://platform.sh/cli/installer | php \
    && echo "source /root/.profile" > /root/.bashrc \
    && wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
    && rm dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/* \
    && rm -rf /tmp/pear

# Blackfire
#RUN export VERSION=`php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;"` \
#    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/${VERSION} \
#    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
#    && mv /tmp/blackfire-*.so `php -r "echo ini_get('extension_dir');"`/blackfire.so \
#    && echo "extension=blackfire.so" > $PHP_INI_DIR/conf.d/blackfire.ini \
#    && echo "blackfire.agent_socket=\${BLACKFIRE_PORT}" >> $PHP_INI_DIR/conf.d/blackfire.ini
