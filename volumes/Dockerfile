FROM php:8.0-fpm-alpine

# Arguments defined in docker-compose.yml
# Install PHP extensions
RUN apk add --no-cache --virtual \
    mysql-client \
    msmtp \
    perl \
    wget \
    procps \
    shadow \
    libzip \
    libpng \
    libjpeg-turbo \
    libwebp \
    freetype \
    icu \
    build-essentials \
    icu-dev \
    icu-libs \
    zlib-dev \
    g++ \
    make \
    automake \
    autoconf \
    libzip-dev \
    libpng-dev \
    libwebp-dev \
    libjpeg-turbo-dev \
    freetype-dev && \
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp --with-xpm; \
    docker-php-ext-install pdo_mysql mysqli mbstring exif gd pcntl bz2 opcache zip bcmath; \
    docker-php-ext-enable pdo_mysql mysqli mbstring exif gd pcntl bz2 opcache zip bcmath; \
    pecl install redis; \
    docker-php-ext-enable redis; \
    apk del build-essentials && rm -rf /usr/src/php*

# Get latest Composer
RUN wget https://getcomposer.org/composer-stable.phar -O /usr/local/bin/composer && chmod +x /usr/local/bin/composer

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u 1000 -d /home/bagus bagus
RUN mkdir -p /home/bagus/.composer && \
    chown -R bagus:bagus /home/bagus

# Set working directory
WORKDIR /var/www

USER bagus 