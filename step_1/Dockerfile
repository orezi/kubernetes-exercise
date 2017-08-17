FROM linuxconfig/lamp

# Install prerequisites 
RUN apt-get update -y
RUN apt-get install -y wget 

# Download and decompress Mediawiki tarball
RUN wget -qO /tmp/mediawiki.tar.gz https://releases.wikimedia.org/mediawiki/1.25/mediawiki-1.25.3.tar.gz
RUN rm -rf /var/www/html
RUN tar xzf /tmp/mediawiki.tar.gz  -C /var/www/
RUN mv /var/www/mediawiki-* /var/www/html
RUN rm /tmp/mediawiki.tar.gz

# Create database
RUN service mysql start; mysqladmin -uadmin -ppass create mediawiki

# Update file ownership
RUN chown -R www-data.www-data /var/www/html

# Apache configuration
ADD 000-default.conf /etc/apache2/sites-available/
RUN a2enmod rewrite
 

# Allow ports
EXPOSE 80

CMD ["supervisord"]
