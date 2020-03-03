FROM php:7.4-apache

RUN apt-get update \
 && apt-get install -y \
        supervisor \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN a2enmod rewrite
RUN echo 'ServerName localhost' >> /etc/apache2/apache2.conf
RUN sed -i 's/CustomLog ${APACHE_LOG_DIR}\/access\.log combined/CustomLog ${APACHE_LOG_DIR}\/access\.log combined env=!dontlog/g' /etc/apache2/conf-available/other-vhosts-access-log.conf
RUN sed -i 's/CustomLog ${APACHE_LOG_DIR}\/access\.log combined/CustomLog ${APACHE_LOG_DIR}\/access\.log combined env=!dontlog/g' /etc/apache2/sites-available/default-ssl.conf
RUN sed -i 's/CustomLog ${APACHE_LOG_DIR}\/access\.log combined/CustomLog ${APACHE_LOG_DIR}\/access\.log combined env=!dontlog/g' /etc/apache2/sites-available/000-default.conf
RUN rm /var/log/apache2/*
USER www-data
RUN touch /var/log/apache2/access.log \
 && touch /var/log/apache2/error.log \
 && touch /var/log/apache2/other_vhosts_access.log
USER root
CMD ["supervisord", "-n"]