FROM php:7.0-fpm

MAINTAINER Ringtail <zhongwei.lzw@alibaba-inc.com>

ENV NGINX_VERSION 1.11.3-1~jessie

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
	&& echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list \
	&& apt-get update -y \
<<<<<<< HEAD
  && apt-get upgrade -y \
=======
  && apt-get upgrade -y\
>>>>>>> 579d058c84e4a7f6949641ebfc22fbaa81a42c9f
	&& apt-get install --no-install-recommends --no-install-suggests -y \
						ca-certificates \
            libmcrypt4 \
            supervisor \
            php-pear \
            curl \
            git \
            unzip \
            libxrender1 \
            libfontconfig \
            libxext6 \
            wget \
            tar \
            pandoc \
<<<<<<< HEAD
            libxrender1 \
            libfontconfig \
	    libxext6 \
=======
            wkhtmltopdf \
>>>>>>> 579d058c84e4a7f6949641ebfc22fbaa81a42c9f
						nginx=${NGINX_VERSION} \
						nginx-module-xslt \
						nginx-module-geoip \
						nginx-module-perl \
						nginx-module-njs \
						gettext-base \
	&& rm -rf /var/lib/apt/lists/*


# Install wkhtmltox
#RUN wget http://download.gna.org/wkhtmltopdf/0.12/0.12.3/wkhtmltox-0.12.3_linux-generic-amd64.tar.xz

#RUN cd /opt && tar zxvf wkhtmltox-0.12.3_linux-generic-amd64.tar.xz

#RUN ln -s /opt/wkhtmltox/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
#RUN ln -s /opt/wkhtmltox/bin/wkhtmltopdf /usr/bin/wkhtmltopdf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
  	&& ln -sf /dev/stderr /var/log/nginx/error.log

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini

# Disable Populating Raw POST Data
# Not needed when moving to PHP 7.
# http://php.net/manual/en/ini.core.php#ini.always-populate-raw-post-data
RUN echo "always_populate_raw_post_data=-1" > $PHP_INI_DIR/conf.d/always_populate_raw_post_data.ini

# Register the COMPOSER_HOME environment variable
ENV COMPOSER_HOME /composer

# Add global binary directory to PATH and make sure to re-export it
ENV PATH /composer/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
    && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

ADD supervisord.conf /etc/supervisord.conf
RUN chown -R www-data:www-data /var/www/html
EXPOSE 80 443

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
