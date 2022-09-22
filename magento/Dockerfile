FROM ubuntu:20.04
ENV NAME_PROJECT magento2

RUN apt update \
    && apt install -y nginx \
    && apt install -y php7.4-fpm php7.4-cli php7.4-common php7.4-curl php7.4-mysql php7.4-gd php7.4-xml php7.4-json php7.4-intl php-pear php7.4-dev php7.4-common php7.4-mbstring php7.4-zip php7.4-soap php7.4-bcmath php7.4-opcache \ 
    php7.4-mbstring \
    && rm /etc/php/7.4/fpm/php.ini \
    && rm /etc/php/7.4/cli/php.ini \
    && rm /etc/nginx/sites-available/default

#import file 
ADD default /etc/nginx/sites-available
ADD magento2 /etc/nginx/sites-available
ADD php.ini /etc/php/7.4/fpm
ADD php.ini /etc/php/7.4/cli

#Configure Elasticsearch on Ubuntu 20.04
#ADD magento_es_auth.conf /etc/nginx/conf.d 

#install Composer1
RUN cd ~ \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer --version=1.10.16 \ 
    && composer selfupdate \
    && composer 

#Activate Your Virtual Host Configuration file And Reload Nginx.
RUN ln -s /etc/nginx/sites-available/magento2 /etc/nginx/sites-enabled/

ADD startup.sh /
WORKDIR /var/www/html
EXPOSE 80
EXPOSE 443
CMD ["sh", "/startup.sh"]