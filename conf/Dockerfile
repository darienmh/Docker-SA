FROM centos/php-56-centos7

USER root

RUN php -v

ADD ../data/php/composer.phar /usr/bin/composer
RUN chmod +x /usr/bin/composer \
&& composer --version

# Install modules
#RUN yum update -y

RUN yum install -y \
    unzip \
    openssl-devel.x86_64 \
    libzip-devel.x86_64 \


#    	libfreetype6-dev \
#    	libjpeg62-turbo-dev \
#    	libpq-dev \
#    	libldap2-dev \
#    	libxslt-dev \
#    	libcurl4-openssl-dev \
#    	libmcrypt-dev \
#    	libicu-dev \

    wkhtmltopdf

RUN pecl install xdebug
RUN pecl install imagick

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/

RUN docker-php-ext-install -j$(nproc) \
	pdo \
	pgsql \
	pdo_pgsql \
	pdo_mysql \
	mysqli \
	soap \
	gd \
	bcmath \
	json \
	xsl \
	zip \
	ldap \
	intl \
	curl \
	mcrypt \
	phar \
	json

CMD ["php56-sa"]