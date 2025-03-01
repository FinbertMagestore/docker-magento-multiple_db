FROM php:7.1-apache

# php extensions to run Magento
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxslt1-dev \
        libicu-dev \
        zlib1g-dev \
        curl \
        git \
    && docker-php-ext-install -j$(nproc) mcrypt xsl intl pdo_mysql soap zip opcache bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Fix permission denied of execute files
RUN chmod +x /usr/local/bin/docker-php-entrypoint

# Expose ports
EXPOSE 80 443

# Back
COPY run-apache /usr/local/bin/
RUN chmod +x /usr/local/bin/run-apache

COPY mysql.php /var/www/html

CMD ["run-apache"]
WORKDIR /var/www/html
