FROM php:8.3-fpm-alpine

#php extension installer
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

#composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
#php extensions
RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions gd xdebug

RUN install-php-extensions pdo pdo_mysql exif gettext intl pdo_pgsql
RUN install-php-extensions xsl shmop sockets sysvmsg sysvsem sysvshm
RUN install-php-extensions opcache zip xdebug redis
RUN install-php-extensions dom xml xmlwriter fileinfo tokenizer

RUN addgroup -g 1000 -S www && \
    adduser -u 1000 -S www -G www

COPY --chown=www:www-data . /var/www

USER www

WORKDIR "/var/www"
