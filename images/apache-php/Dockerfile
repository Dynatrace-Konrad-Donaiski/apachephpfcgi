FROM ubuntu:trusty
MAINTAINER Konrad Donaiski <Konrad.Donaiski@dynatrace.com>

# Install base packages
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -yq install \
        curl \
        apache2 \
	libapache2-mod-php5 \
	libapache2-mod-fcgid \
	php5-cgi \
        php5-mysql \
        php5-mcrypt \
        php5-gd \
        php5-curl \
        php-pear \
        php-apc && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN /usr/sbin/php5enmod mcrypt
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    sed -i "s/variables_order.*/variables_order = \"EGPCS\"/g" /etc/php5/apache2/php.ini

ENV ALLOW_OVERRIDE **False**
RUN /usr/sbin/a2dismod php5
RUN /usr/sbin/a2enmod fcgid

# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh

EXPOSE 80
WORKDIR /app
CMD ["/run.sh"]
