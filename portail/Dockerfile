FROM ubuntu

RUN apt-get update -y && apt-get install -y php7.0 php7.0-dev php7.0-zip php7.0-mbstring curl git subversion

RUN \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

RUN svn co --username 'antony' --password 'amarchi;c2wGVs34' --no-auth-cache https://subversion.ciss.fr/Portail/branches/Evol225/src portail
COPY 10-portail.conf /etc/apache2/sites-enabled/10-portail.conf
WORKDIR portail
COPY auth.json auth.json
RUN composer install
WORKDIR ..

CMD cp -r portail /var/www/html/portail && chmod 777 -R /var/www/html/portail