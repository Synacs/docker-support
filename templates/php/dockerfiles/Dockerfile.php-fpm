FROM php:8.3-fpm

WORKDIR /application

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
RUN install-php-extensions mbstring pgsql pdo_pgsql xml redis raphf bcmath curl

USER "1000:1000"

COPY --chown=1000:1000 src /application
RUN composer install \
    && cp .env.example .env \
    && php artisan key:generate \
    && php artisan migrate

# ENTRYPOINT [ "php-fpm" ]