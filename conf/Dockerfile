FROM centos/php-56-centos7

USER root

RUN php -v

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
&& php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
&& php composer-setup.php \
&& php -r "unlink('composer-setup.php');" \
&& cp composer.phar /usr/bin/composer \
&& chmod +x /usr/bin/composer \
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