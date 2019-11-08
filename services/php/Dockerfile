# Latest version of php-fpm as of November 09, 2019
FROM php:7.3-fpm

# Install libraries for php service (Unrecommended but needed)
RUN apt-get update && apt-get install -y \
    libxml2-dev \
    libssl-dev \
    libpq-dev \
    libbz2-dev \
    libpng-dev \
    libjpeg-dev \
    libgmp-dev \
    libzip-dev \
    git

# Install extensions for php service
RUN docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install bz2 && \
    docker-php-ext-install iconv && \
    docker-php-ext-install calendar && \
    docker-php-ext-install dom && \
    docker-php-ext-install gd && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install pdo pdo_mysql && \
    docker-php-ext-install gmp && \
    docker-php-ext-enable pdo pdo_mysql

# Install APCu for caching
RUN pecl install apcu && \
    echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini

# Install XDebug for PHP Debugging Tools
ARG XDEBUG_ON=false
ARG XDEBUG_REMOTE_HOST=127.0.0.1
RUN if [ ${XDEBUG_ON} = true ]; then \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    echo "xdebug.default_enable = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_autostart = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_connect_back = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.profiler_enable = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_host = ${XDEBUG_REMOTE_HOST}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_port = 9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
;fi

# Create user inside container
RUN groupadd -g 1000 appuser && \
    useradd -r -u 1000 -g appuser appuser

# Make it the default user
USER appuser

# Copy configuration files
COPY ./configuration/php.ini /usr/local/etc/php/php.ini:ro
COPY ./configuration/php-fpm.conf /usr/local/etc/php-fpm.conf:ro
COPY ./configuration/www.conf /usr/local/etc/php-fpm.d/www.conf:ro

# Expose port to host
EXPOSE 9000

CMD ["php-fpm"]
