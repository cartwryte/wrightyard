# This argument defines the PHP version for the image.
# It defaults to 8.4 if no 'PHP_VERSION' build-arg is passed from compose.yaml.
ARG PHP_VERSION=8.4

FROM php:${PHP_VERSION}-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    mariadb-client \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions \
    @composer \
    gd \
    mysqli \
    pdo_mysql \
    zip \
    opcache

# Set working directory
WORKDIR /workspace/.wrightyard/opencart

# Copy and grant execution rights to our entrypoint script
COPY docker/php/docker-wrightyard-entrypoint /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-wrightyard-entrypoint

# Set the entrypoint
ENTRYPOINT ["docker-wrightyard-entrypoint"]

# The default command to run after the entrypoint
CMD ["php-fpm"]
