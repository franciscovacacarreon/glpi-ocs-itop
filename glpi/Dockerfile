# Imagen base de PHP con Apache
FROM php:8.2-apache

# Configuraciones de zona horaria
ENV TZ=America/La_Paz

# Instalar dependencias necesarias y extensiones PHP
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libwebp-dev \
    libfreetype6-dev \
    libicu-dev \
    libxml2-dev \
    libzip-dev \
    libbz2-dev \
    libonig-dev \
    libldap2-dev \
    libsodium-dev \
    unzip \
    curl \
    git \
    && docker-php-ext-install mysqli pdo pdo_mysql gd intl xml zip bz2 exif sodium ldap opcache \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp

# Habilitar mod_rewrite de Apache
RUN a2enmod rewrite

# Copiar la configuración personalizada de PHP
COPY ./glpi-config/php/glpi.ini /usr/local/etc/php/conf.d/glpi.ini

# Montaremos tu proyecto local con docker-compose
WORKDIR /var/www/html
