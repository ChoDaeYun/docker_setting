FROM php:7.2-fpm-alpine

# Install packages
RUN apk --no-cache add \
    bash \
    libzip-dev \
    libpng-dev \
    libjpeg-turbo-dev

# Install php extensions
RUN docker-php-ext-install zip
RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd
RUN docker-php-ext-install pdo_mysql

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ARG INSTALL_MYSQLI=true
RUN if [ ${INSTALL_MYSQLI} = true ]; then \
    docker-php-ext-install mysqli && \
    docker-php-ext-enable mysqli \
;fi


#ARG INSTALL_XDEBUG=true
#RUN if [ ${INSTALL_XDEBUG} = true ]; then \
#    # Install the xdebug extension
#    pecl install xdebug && \
#    docker-php-ext-enable xdebug \
#;fi

## Copy xdebug configration for remote debugging
#COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini