#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM php:8.1-fpm

# Arguments defined in docker-compose.yml
ARG user
ARG uid

# Set working directory
WORKDIR /var/www/laravel

# Install system dependencies
RUN apt-get update && apt-get install -y \
    apt-utils\
    libonig-dev\
    libpng-dev \
    libzip-dev\
    libxml2-dev \
    libwebp-dev \
    libxpm-dev \
    build-essential \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libmagickwand-dev \
    && apt-get clean all

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg
# RUN docker-php-ext-configure gd \
#     --with-gd \
#     --with-webp-dir \
#     --with-jpeg-dir \
#     --with-png-dir \
#     --with-zlib-dir \
#     --with-xpm-dir \
#     --with-freetype-dir

RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.16

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install nodejs -y
RUN apt-get install -y npm

# RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
# RUN apt-get install nodejs

# Verify installation
RUN command -v node
RUN command -v npm

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]

# Display versions installed
RUN php -v
RUN composer --version
RUN node -v
RUN npm -v