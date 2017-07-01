FROM php:5.6-apache
MAINTAINER Artur Luiz Oliveira <contato@arturluiz.com>

# PHP Dependencies
RUN apt-get update \
    && apt-get install zlib1g-dev libxml2-dev -y \
    && docker-php-ext-install mysqli mysql zip soap

# Cloning and Cleaning OJS and PKP-LIB git repositories
RUN wget https://github.com/pkp/pkp-lib/archive/ojs-2_4_8-2.zip \
    && rm -fr /var/www/html/* \
    && unzip ojs-2_4_8-2.zip -d /var/www/html/ \
    && git clone -v --recursive --progress https://github.com/arturluizbr/ojs.git /var/www/html \
    && cd /var/www/html \
    && find . | grep .git | xargs rm -rf 

# Configuring OJS
RUN cp config.TEMPLATE.inc.php config.inc.php \
    && mkdir -p /var/www/files/ \
    && chown -R www-data:www-data /var/www/ \
