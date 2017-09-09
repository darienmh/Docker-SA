FROM centos/php-56-centos7

#COPY composer.phar /usr/local/bin/composer

RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN pecl install imagick && docker-php-ext-enable imagick

# Install Composer
RUN composer --version

# Install modules
RUN apt-get update -y

RUN apt-get install -y --force-yes \
    unzip \
    libssl-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpq-dev \
    libzip-dev \
    libldap2-dev \
    libxslt-dev \
    libcurl4-openssl-dev \
    libmcrypt-dev \
    libicu-dev \
    imagemagick \
    libsqlite3-dev \
    wkhtmltopdf

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

CMD ["php63-ce"]