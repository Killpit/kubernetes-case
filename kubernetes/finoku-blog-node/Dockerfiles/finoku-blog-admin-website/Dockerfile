FROM php:8.2-apache-fpm

# Install additional required packages
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    unzip \
    git \
    curl \
    libpng-dev \
    libjpeg-dev \
    libwebp-dev \
    libicu-dev \
    libxft2-font-config \
    freetype2-config

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set working directory
WORKDIR /var/www/html

# Copy composer dependencies
COPY composer.json composer.lock ./

# Install dependencies
RUN composer install --no-dev

# Clean up apt cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy the rest of the application
COPY . .

# Adjust PHP configuration (optional)
COPY php.ini /usr/local/etc/php/php.ini

# Expose port 80
EXPOSE 80