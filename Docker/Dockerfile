FROM php:8.1-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    cron



# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd intl 

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY Docker/php/php.ini   $PHP_INI_DIR/conf.d/

# Set working directory
WORKDIR /var/www

# copy the project
COPY . /var/www


# Add crontab file in the cron directory
ADD Docker/worker/crontab /etc/cron.d/crontab

# Give execution rights on the cron job
RUN chmod 0644 /etc/cron.d/crontab



