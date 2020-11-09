FROM php:7.4-fpm
 
RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini
ARG USER_ID
ARG GROUP_ID

RUN apt-get update && apt-get install -y \
libonig-dev \
libzip-dev \
gnupg2 \
curl \
wget \
git \
sudo \
mc \
build-essential \
libxslt-dev \
libicu-dev \
libmcrypt-dev \
libxml2-dev \
libpq-dev \
&& docker-php-ext-install -j$(nproc) iconv mbstring pgsql pdo_pgsql zip \
&& pecl install xdebug-2.9.6 \
&& docker-php-ext-enable xdebug \
&& docker-php-ext-install mysqli

#RUN apt-get install --reinstall make

RUN wget https://get.symfony.com/cli/installer -O - | bash

RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN curl -sS https://getcomposer.org/installer | php -- \
--install-dir=/usr/bin --filename=composer && chmod +x /usr/bin/composer

RUN usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data
RUN   git config --global user.email "romzhr@gmail.com" \
&& git config --global user.name "romnhl" && chown www-data:www-data /var/www


WORKDIR /www/app
