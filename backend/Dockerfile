FROM php:8.2-apache

COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer
COPY ./backend/000-default.conf /etc/apache2/sites-available/000-default.conf

RUN apt-get update \
    && apt-get install -y \
    git \
    zip \
    unzip \
    libzip-dev \
    vim \
    libpng-dev \
    libpq-dev \
    libfreetype6-dev \
    libjpeg-dev \
    libonig-dev \
    && docker-php-ext-install pdo pdo_pgsql pgsql zip

WORKDIR /var/www

RUN echo "Listen 8080" >> /etc/apache2/ports.conf && \
    a2enmod rewrite