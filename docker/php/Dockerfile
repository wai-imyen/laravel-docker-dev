# basic enviroment
FROM php:8.2-fpm

# Set working directory
WORKDIR /var/www

# Install dependencies
RUN apt-get update; \
    apt-get install -y --no-install-recommends \
        build-essential \
        libpq-dev \
        libpng-dev \
        libjpeg62-turbo-dev \
        libfreetype6-dev \
        libwebp-dev \
        locales \
        zip \
        vim \
        unzip \
        git \
        curl \
        libonig-dev \
        libicu-dev \
        zlib1g-dev \
        libzip-dev  && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl

# jpegoptim
RUN apt-get update; \
    apt-get install -y jpegoptim optipng pngquant gifsicle

# gd
RUN docker-php-ext-configure gd \
            --with-jpeg \
            --with-webp \
            --with-freetype; \
    docker-php-ext-install -j$(nproc) gd

# imagick
RUN apt-get install -y --no-install-recommends libmagickwand-dev && \
    pecl install imagick && \
    docker-php-ext-enable imagick

# intl
RUN docker-php-ext-configure intl && docker-php-ext-install intl

# redis
RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

# rdkafka
RUN apt-get install -y librdkafka-dev && \
    pecl install rdkafka && \
    docker-php-ext-enable rdkafka

# opcache
RUN docker-php-ext-install opcache
COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# config
COPY laravel.ini /usr/local/etc/php/conf.d

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

USER root

# Configure non-root user.
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

RUN groupmod -o -g ${PGID} www-data && \
    usermod -o -u ${PUID} -g www-data www-data

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
