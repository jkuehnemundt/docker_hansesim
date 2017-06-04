FROM php:fpm

MAINTAINER Jannik Kühnemundt <jkuehnemundt@gmail.com>

RUN apt-get update && apt-get install -y \
        git \
        zip \
		wget \
        nodejs \
        npm \
        build-essential \
        libpng12-dev libjpeg-dev libpq-dev \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
        && docker-php-ext-install gd mbstring pdo pdo_mysql pdo_pgsql

COPY symfony.pool.conf  /usr/local/etc/

RUN pecl install xdebug \
            && docker-php-ext-enable xdebug

ENV XDEBUGINI_PATH=/usr/local/etc/php/conf.d/xdebug.ini
RUN echo "zend_extension="`find /usr/local/lib/php/extensions/ -iname 'xdebug.so'` > $XDEBUGINI_PATH
COPY xdebug.ini /tmp/xdebug.ini
RUN cat /tmp/xdebug.ini >> $XDEBUGINI_PATH
RUN echo "xdebug.remote_host="`/sbin/ip route|awk '/default/ { print $3 }'` >> $XDEBUGINI_PATH
RUN rm /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN npm install -g bower && \
    echo '{ "allow_root": true }' > /root/.bowerrc
RUN npm install -g uglifycss
RUN npm install -g uglify-js
RUN npm install -g less
RUN ln -s "$(which nodejs)" /usr/local/bin/node

RUN usermod -u 1000 www-data


WORKDIR "/home/student/htdocs/hansesim"
CMD ["php-fpm", "-F"]
#RUN php app/console doctrine:schema:update --force
#RUN php app/console doctrine:fixtures:load
