FROM linuxconfig/apache

# Install prerequisites 
RUN apt-get update -y

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get install -y wget libapache2-mod-php5 php5-mysql php5-gd php-apc php5-mcrypt

# Download and decompress Mediawiki tarball
RUN wget -qO /tmp/mediawiki.tar.gz https://releases.wikimedia.org/mediawiki/1.25/mediawiki-1.25.3.tar.gz
RUN rm -rf /var/www/html
RUN tar xzf /tmp/mediawiki.tar.gz  -C /var/www/
RUN mv /var/www/mediawiki-* /var/www/html
RUN rm /tmp/mediawiki.tar.gz


# Update file ownership
RUN chown -R www-data.www-data /var/www/html

# Apache configuration
ADD 000-default.conf /etc/apache2/sites-available/
RUN a2enmod rewrite
 

# Allow ports
EXPOSE 80

