FROM php:8.1-apache

# Instalar extensiones requeridas por iTop
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libwebp-dev \
    libfreetype6-dev \
    libicu-dev \
    libxml2-dev \
    libzip-dev \
    unzip \
    git \
    && docker-php-ext-configure gd \
        --with-jpeg \
        --with-webp \
        --with-freetype \
    && docker-php-ext-install \
        gd \
        intl \
        mysqli \
        pdo \
        pdo_mysql \
        zip \
        opcache \
        soap \
    && a2enmod rewrite

# Configurar Apache (importante para iTop)
RUN printf "\n<Directory /var/www/html/>\n\
    AllowOverride All\n\
    </Directory>\n" >> /etc/apache2/apache2.conf


# Configurar PHP: aumentar memoria, tiempo y upload max
RUN echo "memory_limit=512M"            >  /usr/local/etc/php/conf.d/itop.ini \
 && echo "upload_max_filesize=100M"     >> /usr/local/etc/php/conf.d/itop.ini \
 && echo "post_max_size=100M"           >> /usr/local/etc/php/conf.d/itop.ini \
 && echo "max_execution_time=300"       >> /usr/local/etc/php/conf.d/itop.ini \
 && echo "max_input_time=300"           >> /usr/local/etc/php/conf.d/itop.ini

# Ajustar permisos para que iTop pueda escribir en conf/, data/ y log/
RUN chown -R www-data:www-data /var/www

# Puerto
EXPOSE 80

CMD ["apache2-foreground"]
