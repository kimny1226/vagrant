FROM php:7.2-apache
# RUN ls -l /vagrant/sources/
# COPY /vagrant/sources/ /var/www/html/
# RUN docker-php-ext-install pdo_mysql
# RUN apt-get update && \
#     docker-php-ext-install pdo_mysql mysqli mbstring

RUN apt-get update && apt-get install -y \
        git \
        unzip \
        zlib1g-dev \
        libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install \
        zip \
        intl \
        mbstring \
        pdo_mysql \
    && pecl install xdebug \
    && pecl install apcu \
    && docker-php-ext-enable \
        xdebug \
        apcu \
        opcache \
    && a2enmod rewrite \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# SSL対応
# ssl-cert オレオレ証明書用
RUN apt-get update && apt-get install -y \
        libssl-dev \
        openssl \
        ssl-cert \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && a2enmod ssl \
    && a2ensite default-ssl

# RUN curl -s http://getcomposer.org/installer | php && \
#     echo "export PATH=${PATH}:/var/www/vendor/bin" >> ~/.bashrc && \
#     mv composer.phar /usr/local/bin/composer
RUN useradd -u 1000 -m docker
ENV APACHE_RUN_USER docker
ENV APACHE_RUN_GROUP docker
