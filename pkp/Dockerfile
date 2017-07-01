FROM php:5.6-apache
MAINTAINER Artur Luiz Oliveira <contato@arturluiz.com>

# PHP Dependencies
RUN apt-get update \
    && apt-get install zlib1g-dev libxml2-dev wget unzip vim -y \
    && docker-php-ext-install mysqli mysql zip soap

# Cloning and Cleaning OJS and PKP-LIB git repositories
RUN wget https://github.com/pkp/ojs/archive/ojs-2_4_8-0.zip -O ojs.zip \
    && wget https://github.com/pkp/pkp-lib/archive/ojs-2_4_8-0.zip -O lib.zip \
    && unzip ojs.zip -d /var/www/html/ \
    && mv ojs-ojs-2_4_8-0/* . \
    && rm -rf ojs.zip \ 
    && rm -rf ojs-ojs-2_4_8-0 \
    && mkdir Test \ 
    && mv lib.zip Test/ \ 
    && cd Test/ \
    && wget https://github.com/swordapp/swordappv2-php-library/archive/master.zip -O sword2.zip \
    && unzip lib.zip \
    && unzip sword2.zip \
    && cd /var/www/html \
    && mv Test/pkp-lib-ojs-2_4_8-0/* lib/pkp/ \
    && mv Test/swordappv2-php-library-master/* lib/pkp/lib/swordappv2/ \
    && cd /var/www/html \
    && rm -rf Test \
    && cd plugins/reports/counter/classes/COUNTER/ \
    && wget https://github.com/ulsdevteam/COUNTER/archive/master.zip -O counter.zip \
    && unzip counter.zip \
    && mv COUNTER-master/* . \
    && rm -rf COUNTER-master \
    && rm counter.zip \
    && cd /var/www/html \
    && cd lib/password_compat \
    && wget https://github.com/ircmaxell/password_compat/archive/master.zip -O pass.zip \
    && unzip pass.zip \
    && mv password_compat-master/* . \
    && rm -rf password_compat-master \
    && rm pass.zip \
    && cd /var/www/html \
    && find . | grep .git | xargs rm -rf 

# Configuring OJS
RUN cp config.TEMPLATE.inc.php config.inc.php \
    && chmod ug+rw config.inc.php \
    && mkdir -p /var/www/files/ \
    && chown -R www-data:www-data /var/www/ \

