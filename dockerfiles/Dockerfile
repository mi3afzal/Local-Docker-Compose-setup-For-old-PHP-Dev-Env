FROM centos:7

LABEL maintainer="mi3afzal@gmail.com"

# Install some must-haves
RUN yum -y install vim wget sendmail
RUN yum -y install libtool make automake autoconf nasm libpng-static
RUN yum -y install git
RUN git --version

# Install PHP 7.1 on CentOS
#RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
#	&& rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
#RUN yum install yum-utils
#RUN yum-config-manager --enable remi-php74

RUN yum install epel-release -y
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

#RUN yum -y install php \
RUN yum -y --enablerepo=remi-php74 install php \
					         php-bcmath \
					         php-cli \
					         php-common \
					         php-curl \
					         php-fpm \
					         php-gd \
					         php-ldap \
					         php-imap \
					         php-intl \
					         php-mbstring \
					         php-mcrypt \
					         php-mysqlnd \
					         php-opcache \
					         php-pdo \
					         php-pear \
					         php-pecl-apcu \
					         php-pecl-imagick \
					         php-pgsql \
					         php-process \
					         php-pspell \
					         php-recode \
					         php-soap \
					         php-tidy \
                             php-zip \
					         php-xml

RUN php -v

# Prepare PHP environment
COPY config/php/php-fpm.conf /etc/php-fpm.conf
COPY config/php/www.conf /etc/php-fpm.d/www.conf
COPY config/php/php.ini /usr/local/etc/php/php.ini
COPY config/php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer
RUN composer --version

# Install Node.js
RUN curl -sL https://rpm.nodesource.com/setup_7.x | bash -
RUN yum -y install nodejs
RUN yum list installed nodejs
RUN node -v

# Final update and clean up
RUN yum -y update
RUN yum clean all

# Define work directory
WORKDIR /var/www/html/

# Expose ports
EXPOSE 9000

CMD ["php-fpm", "-F", "-O"]
