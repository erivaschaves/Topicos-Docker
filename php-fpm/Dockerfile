FROM php:7.1.9-fpm
 
MAINTAINER Erivaldo Chaves <erivaldo.chaves@souunit.com.br>


RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl \
    openssl \
    nano


RUN apt-get install -y --no-install-recommends libpq-dev libz-dev \
 && docker-php-ext-install pcntl \
 && docker-php-ext-install session \
 && docker-php-ext-install phar \
 && docker-php-ext-install iconv \
 && docker-php-ext-install pdo



ARG INSTALL_GD=false
RUN if [ ${INSTALL_GD} = true ]; then \
    # Install gd and requirements
    apt-get install -y --no-install-recommends libjpeg-dev libpng12-dev libfreetype6-dev \
 && docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 \
 && docker-php-ext-install gd \
;fi



ARG INSTALL_COMPRESSION=false
RUN if [ ${INSTALL_COMPRESSION} = true ]; then \
    # Install zip, bz2 and requirements
    apt-get install -y --no-install-recommends libbz2-dev zlib1g-dev \
 && docker-php-ext-install zip \
    bz2 \
;fi


ARG INSTALL_FTP=false
RUN if [ ${INSTALL_FTP} = true ]; then \
    
    apt-get install -y --no-install-recommends libssl-dev \
 && docker-php-ext-install ftp \
;fi



ARG INSTALL_MCRYPT=false
RUN if [ ${INSTALL_MCRYPT} = true ]; then \
    
    apt-get install -y --no-install-recommends libmcrypt-dev \
 && docker-php-ext-install mcrypt \
;fi



ARG INSTALL_MBSTRING=false
RUN if [ ${INSTALL_MBSTRING} = true ]; then \
    
    docker-php-ext-install mbstring \
;fi



ARG INSTALL_PDO_MYSQL=false
RUN if [ ${INSTALL_PDO_MYSQL} = true ]; then \
    
    docker-php-ext-install pdo_mysql \
;fi



ARG INSTALL_PDO_POSTGRESQL=false
RUN if [ ${INSTALL_PDO_POSTGRESQL} = true ]; then \
    
    docker-php-ext-install pdo_pgsql \
;fi



ARG INSTALL_MYSQLI=false
RUN if [ ${INSTALL_MYSQLI} = true ]; then \
    
    docker-php-ext-install mysqli \
;fi



ARG INSTALL_BCMATH=false
RUN if [ ${INSTALL_BCMATH} = true ]; then \
    
    docker-php-ext-install bcmath \
;fi



ARG INSTALL_OPCACHE=false
RUN if [ ${INSTALL_OPCACHE} = true ]; then \
    docker-php-ext-install opcache \
;fi


COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini



ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    
    pecl install xdebug \
    docker-php-ext-enable xdebug \
;fi


COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini



ARG INSTALL_COMPOSER=false
RUN if [ ${INSTALL_COMPOSER} = true ]; then \
    # Install the composer
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
;fi


COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini



ARG INSTALL_TOKENIZER=false
RUN if [ ${INSTALL_TOKENIZER} = true ]; then \
    
    docker-php-ext-install tokenizer \
;fi



ARG INSTALL_JSON_XML=false
RUN if [ ${INSTALL_JSON_XML} = true ]; then \
    
    apt-get install -y --no-install-recommends libxml2-dev libxslt-dev \
 && docker-php-ext-install json \
    xml \
    dom \
    xmlrpc \
    xsl \
;fi





ARG INSTALL_INTL=false
RUN if [ ${INSTALL_INTL} = true ]; then \
    
    apt-get install -y --no-install-recommends zlib1g-dev libicu-dev g++ \
 && docker-php-ext-configure intl \
 && docker-php-ext-install intl \
;fi


RUN rm -rf /var/lib/apt/lists/*


RUN chown -R root:www-data /var/www/html
RUN chmod u+rwx,g+rx,o+rx /var/www/html
RUN find /var/www/html -type d -exec chmod u+rwx,g+rx,o+rx {} +
RUN find /var/www/html -type f -exec chmod u+rw,g+rw,o+r {} +

CMD ["php-fpm"]

EXPOSE 9000
