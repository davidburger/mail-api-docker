FROM php:7.1-fpm

RUN  apt-get update && apt-get install -y build-essential ca-certificates \
 git curl libcurl3 libcurl3-dev \
 openssl tar \
 libpq-dev

RUN docker-php-ext-install pdo_mysql pdo_pgsql zip

RUN apt-get upgrade -y sendmail && rm -rf /var/lib/apt/lists/*

#install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

RUN echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/mail.ini

#reduce image size
RUN apt-get autoremove -y
RUN apt-get clean
RUN apt-get autoclean

RUN usermod -u 1000 www-data

#container_IP container_ID container_ID.localdomain
#RUN echo -e "$(hostname -i)\t$(hostname) $(hostname).localhost $(hostname).localdomain" >> /etc/hosts
#RUN /etc/init.d/sendmail restart

# Add the application code into the container
ADD . /var/www/mail-api

WORKDIR /var/www/mail-api
