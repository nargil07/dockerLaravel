FROM ubuntu

RUN apt-get update -y && apt-get install apache2 -y

EXPOSE 80
RUN a2enmod rewrite
RUN a2enmod proxy_fcgi

RUN rm /var/www/html/index.html
RUN rm /etc/apache2/sites-enabled/000-default.conf

COPY index.php /var/www/html/index.php

RUN chmod 777 -R /var/log/apache2

CMD /usr/sbin/apache2ctl -D FOREGROUND