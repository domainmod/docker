FROM php:7.4-apache
ENV LOCALE1="en_CA.UTF-8"
ENV LOCALE2="en_US.UTF-8"
ENV LOCALE3="de_DE.UTF-8"
ENV LOCALE4="es_ES.UTF-8"
ENV LOCALE5="fr_FR.UTF-8"
ENV LOCALE6="it_IT.UTF-8"
ENV LOCALE7="nl_NL.UTF-8"
ENV LOCALE8="pl_PL.UTF-8"
ENV LOCALE9="pt_PT.UTF-8"
ENV LOCALE10="ru_RU.UTF-8"
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN apt-get update \
    && apt-get install -y cron curl gettext git libxml2 libxml2-dev locales tzdata \
    && apt-get clean -y \
    && docker-php-ext-install gettext mysqli pdo pdo_mysql simplexml
RUN cp /usr/share/zoneinfo/America/Vancouver /etc/localtime \
    && echo "America/Vancouver" > /etc/timezone
COPY php.ini-production /usr/local/etc/php/php.ini
COPY cron /etc/cron.d/cron
RUN chmod 0644 /etc/cron.d/cron
RUN crontab /etc/cron.d/cron
RUN mkdir -p /var/log/cron
RUN sed -i 's/^exec /service cron start\n\nexec /' /usr/local/bin/apache2-foreground
RUN sed -i -e "s/# $LOCALE1/$LOCALE1/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE2/$LOCALE2/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE3/$LOCALE3/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE4/$LOCALE4/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE5/$LOCALE5/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE6/$LOCALE6/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE7/$LOCALE7/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE8/$LOCALE8/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE9/$LOCALE9/" /etc/locale.gen
RUN sed -i -e "s/# $LOCALE10/$LOCALE10/" /etc/locale.gen
RUN locale-gen
RUN echo "LANG=$LOCALE1" > /etc/default/locale
ENV LANG $LOCALE1
ENV LC_ALL $LOCALE1
RUN cd /var/www/html \
    && git clone https://github.com/domainmod/domainmod.git . \
    && git pull
COPY config.inc.php /var/www/html/_includes
RUN chmod 777 /var/www/html/temp
RUN service apache2 restart
EXPOSE 80 443
