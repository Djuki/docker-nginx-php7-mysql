FROM php:7.4-fpm

RUN useradd -u 1000 local

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        apt-utils \
        libxml2-dev \
        zlib1g-dev \
        zip \
        libcurl4 \
        libpcre3-dev \
        libcurl4-openssl-dev \
        libonig-dev

RUN docker-php-ext-install -j$(nproc) iconv pdo_mysql mbstring
RUN docker-php-ext-install mysqli
#RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install soap
#RUN docker-php-ext-install zip
RUN docker-php-ext-install intl
RUN docker-php-ext-install exif
RUN docker-php-ext-install pcntl
RUN pecl install mongodb && docker-php-ext-enable mongodb

RUN apt-get install -y git

RUN apt-get install -y tidy libtidy-dev
RUN docker-php-ext-install -j$(nproc) tidy

RUN docker-php-ext-configure bcmath \
    && docker-php-ext-install -j$(nproc) bcmath

RUN pecl install redis && docker-php-ext-enable redis    

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

COPY xdebug-3.1.6.tgz /usr/src/php/ext/xdebug.tgz
RUN tar -xf /usr/src/php/ext/xdebug.tgz -C /usr/src/php/ext/ && \
    rm /usr/src/php/ext/xdebug.tgz && \
    docker-php-ext-install xdebug-3.1.6
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

#ENV NODE_VERSION=8.11.4
#RUN apt install -y curl
#RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
#ENV NVM_DIR=/root/.nvm
#RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
#RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
#RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
#ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
#RUN node --version
#RUN npm --version

# to include ioncube support, uncomment the next two lines
#COPY ioncube/ioncube_loader_lin_7.1.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/ioncube_loader_lin_7.1.so
#COPY ioncube.ini /usr/local/etc/php/php.ini