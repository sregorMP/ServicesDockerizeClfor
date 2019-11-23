FROM php:7-fpm-alpine
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
RUN apk add --no-cache openldap-dev mariadb-dev libxml2-dev libpng-dev curl-dev imap-dev
RUN wget https://pecl.php.net/get/apcu -O /tmp/apcu.tar.gz \
    && mkdir -p /usr/src/php/ext/apcu \
    && tar xf /tmp/apcu.tar.gz -C /usr/src/php/ext/apcu --strip-components=1 \
    && docker-php-ext-configure apcu && docker-php-ext-install -j"$(nproc)" apcu \
    && rm /tmp/apcu.tar.gz
RUN wget https://pecl.php.net/get/apcu_bc -O /tmp/apcu_bc.tar.gz \
    && mkdir -p /usr/src/php/ext/apcu-bc \
    && tar xf /tmp/apcu_bc.tar.gz -C /usr/src/php/ext/apcu-bc --strip-components=1 \
    && docker-php-ext-configure apcu-bc && docker-php-ext-install -j"$(nproc)" apcu-bc \
    && rm /tmp/apcu_bc.tar.gz
RUN rm /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini && \
    echo extension=apcu.so > /usr/local/etc/php/conf.d/20-php-ext-apcu.ini
RUN docker-php-ext-configure ldap && docker-php-ext-install ldap
RUN docker-php-ext-configure mysqli && docker-php-ext-install mysqli
RUN docker-php-ext-configure xml && docker-php-ext-install xml
RUN docker-php-ext-configure xmlrpc && docker-php-ext-install xmlrpc
RUN docker-php-ext-configure opcache && docker-php-ext-install opcache
RUN docker-php-ext-configure gd && docker-php-ext-install gd
RUN docker-php-ext-configure curl && docker-php-ext-install curl
RUN docker-php-ext-configure mbstring && docker-php-ext-install mbstring
RUN docker-php-ext-configure imap && docker-php-ext-install imap
RUN echo "date.timezone = America/Fortaleza" > /usr/local/etc/php/conf.d/timezone.ini
ENV tz="America/Fortaleza"
RUN apk add --no-cache  tzdata  \
    && ln -snf /usr/share/zoneinfo/$tz /etc/localtime \ 
    && echo $tz > /etc/timezone