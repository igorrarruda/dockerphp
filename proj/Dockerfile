FROM php:5.6-apache
RUN apt-get update; \
    apt-get -y upgrade;
RUN docker-php-ext-install pdo_mysql

COPY certs/dev.crt /etc/apache2/ssl/dev.crt
COPY certs/dev.key /etc/apache2/ssl/dev.key
COPY .apache-config/dev.conf /etc/apache2/sites-available/default-ssl.conf

# Copy apache vhost file to proxy php requests to php-fpm container
# COPY .apache-config/demo.apache.conf /etc/apache2/httpd.conf
# RUN echo "Include /etc/apache2/demo.apache.conf" \
#    >> /etc/apache2/httpd.conf

RUN a2enmod rewrite
RUN a2ensite default-ssl
RUN a2enmod ssl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

EXPOSE 80
EXPOSE 443