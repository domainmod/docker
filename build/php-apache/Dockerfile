FROM php:7.3-apache
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN apt-get update \
    && apt-get install -y curl gettext git libxml2 libxml2-dev openssl \
    && apt-get clean -y \
    && docker-php-ext-install mysqli pdo pdo_mysql simplexml
RUN git clone https://github.com/domainmod/domainmod.git /var/www/html
COPY config.inc.php /var/www/html/_includes
RUN chmod 777 /var/www/html/temp
RUN service apache2 restart
EXPOSE 80 443
