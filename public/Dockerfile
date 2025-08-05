FROM php:8.2-fpm

# Instalacja zależności systemowych
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl \
    libzip-dev \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Instalacja Composera
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Ustawienie katalogu roboczego
WORKDIR /var/www

# Kopiowanie plików projektu
COPY . .

# Instalacja zależności PHP (prod)
RUN composer install --no-dev --optimize-autoloader

# Ustawienia uprawnień
RUN chown -R www-data:www-data /var/www \
    && chmod -R 755 /var/www/storage

# Ustawienie portu
EXPOSE 8000

# Start serwera Laravel
CMD php artisan serve --host=0.0.0.0 --port=8000