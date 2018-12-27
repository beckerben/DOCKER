FROM php:5-apache
RUN apt-get update -y \
  && rm /etc/apt/preferences.d/no-debian-php \
  && apt-get install -y \
    libxml2-dev \
    php-soap \
  && apt-get clean -y \
  && docker-php-ext-install soap mysql
 
VOLUME /var/www/html

ENV WORDPRESS_UPSTREAM_VERSION 3.2.1
ENV WORDPRESS_VERSION 3.2.1


# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
RUN curl -o wordpress.tar.gz -SL https://wordpress.org/wordpress-${WORDPRESS_UPSTREAM_VERSION}.tar.gz  \
	&& tar -xzf wordpress.tar.gz -C /usr/src/ \
	&& rm wordpress.tar.gz \
	&& chown -R www-data:www-data /usr/src/wordpress

COPY docker-entrypoint.sh /entrypoint.sh

# grr, ENTRYPOINT resets CMD now
ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]
