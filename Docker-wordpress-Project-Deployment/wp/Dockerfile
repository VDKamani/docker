FROM ubuntu:22.04

RUN \
apt update && \
apt install -y apache2 && \
service apache2 start

RUN apt-get update -y && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php -y && \
    apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    php8.1 libapache2-mod-php8.1 php8.1-mysql php8.1-xml php8.1-curl php8.1-gd php8.1-mbstring php8.1-zip php8.1-soap php8.1-intl php8.1-pdo

RUN \
apt-get install -y unzip wget curl && \
rm /var/www/html/index.html && \
chown -R www-data:www-data /var/www && \
usermod -a -G www-data root && \
usermod -a -G root www-data && \
a2enmod rewrite && \
service apache2 restart

RUN echo '<VirtualHost *:80>\n\
\n\
    ServerAdmin webmaster@localhost\n\
    DocumentRoot /var/www/html\n\
\n\
    <Directory /var/www/html>\n\
        AllowOverride All\n\
    </Directory>\n\
\n\
    ErrorLog ${APACHE_LOG_DIR}/wp_error.log\n\
    CustomLog ${APACHE_LOG_DIR}/wp_access.log combined\n\
\n\
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf

RUN apt-get update && apt-get install -y sed

RUN a2enmod php8.1

RUN  service apache2 restart 

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]

