FROM php:8.2-fpm-alpine

# Install system dependencies
RUN apk add --no-cache \
  bash \
  nginx \
  php82-cli \
  php82-fpm \
  php82-pdo_pgsql \
  php82-mbstring \
  php82-xml \
  php82-dom \
  php82-curl \
  php82-zip \
  php82-gd \
  php82-ctype \
  php82-session \
  php82-tokenizer

# Copy nginx configuration
COPY ./nginx/default.conf /etc/nginx/conf.d/

# Copy code
COPY . /var/www/html

# Set permissions
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Expose port
EXPOSE 80

# Set working directory
WORKDIR /var/www/html

# Install Composer dependencies
RUN composer install --no-dev --optimize-autoloader

# Start services
CMD ["/bin/bash", "-c", "php artisan migrate && nginx && php-fpm"]