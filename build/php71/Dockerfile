FROM daocloud.io/library/php:7.1.8-fpm
MAINTAINER wuyihao <303440188@qq.com>

ARG CHANGE_SOURCE=true
ARG INSTALL_TIDEWAYS=true

# Change China Sources
COPY sources.list /etc/apt/china.sources.list
RUN if [ ${CHANGE_SOURCE} = true ]; then \
	mv /etc/apt/sources.list /etc/apt/source.list.bak && mv /etc/apt/china.sources.list /etc/apt/sources.list \
;fi

#Include yii framework
#RUN echo 'include_path = "/var/www/php-framework/yii"' >> /usr/local/etc/php/php.ini

## Update Ubuntu
RUN apt-get update

# Install Base Components
RUN apt-get install -y --no-install-recommends libpng-dev libjpeg-dev libfreetype6-dev ntpdate cron vim unzip git wget


####################################################################################
# Install Extension
####################################################################################
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd pdo_mysql gettext bcmath

#################### 方式一

## 安装 tideways
RUN if [ ${INSTALL_TIDEWAYS} = true ]; then \
    echo 'deb http://s3-eu-west-1.amazonaws.com/qafoo-profiler/packages debian main' > /etc/apt/sources.list.d/tideways.list \
    && wget -qO - https://s3-eu-west-1.amazonaws.com/qafoo-profiler/packages/EEB5E8F4.gpg | apt-key add - \
    && apt-get update \
    && apt-get install tideways-php tideways-daemon \
#    && cd /var/www \
#    && git clone https://github.com/laynefyc/xhgui-branch.git \
#    && cd /var/www/xhgui-branch \
#    && php install.php \
;fi

# Swoole
COPY swoole-2.2.0.tgz /home/swoole.tgz
RUN pecl install /home/swoole.tgz \
		&& docker-php-ext-enable swoole


# Mongodb
COPY mongodb-1.4.2.tgz /home/mongodb.tgz
RUN pecl install /home/mongodb.tgz \
		&& docker-php-ext-enable mongodb


# GeoIp
RUN apt-get install -y libgeoip-dev
COPY geoip-1.1.1.tgz /home/geoip.tgz
RUN tar -xvf /home/geoip.tgz -C /home \
	&& cd /home/geoip-1.1.1 \
	&& phpize \
	&& ./configure \
	&& make \
	&& make install \
	&& docker-php-ext-enable geoip

RUN mkdir -p /usr/share/GeoIP
ADD GeoLiteCity.dat /usr/share/GeoIP/GeoIPCity.dat

# Memcached
RUN apt-get install -y libmemcached-dev zlib1g-dev
COPY memcached-3.0.4.tgz /home/memcached.tgz
RUN pecl install /home/memcached.tgz \ 
		&& docker-php-ext-enable memcached

# Xdebug
COPY xdebug-2.6.0.tgz /home/xdebug.tgz
RUN pecl install /home/xdebug.tgz \ 
		&& docker-php-ext-enable xdebug



# Redis
COPY redis-4.0.0.tgz /home/redis.tgz
RUN pecl install /home/redis.tgz \ 
		&& docker-php-ext-enable redis


#Phalcon
COPY cphalcon.tgz /home/cphalcon.tgz
RUN tar -xvf /home/cphalcon.tgz -C /home \
		&& cd /home/cphalcon/build \
		&& ./install \ 
		&& docker-php-ext-enable phalcon


### php composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \     
		&& php composer-setup.php \     
		&& php -r "unlink('composer-setup.php');" \       
		&& mv composer.phar /usr/local/bin/composer \     
		&& composer config -g repo.packagist composer https://packagist.phpcomposer.com


##################### 方式二 需要网络能访问 https://pecl.php.net/  ################################
# Memcached
#RUN apt-get install -y libmemcached-dev zlib1g-dev \
#		&& pecl install memcached \
#		&& docker-php-ext-enable memcached

#GeoIp
#RUN apt-get install -y libgeoip-dev \
#		&& pecl install geoip-1.1.1 \
#		&& docker-php-ext-enable geoip
#RUN mkdir -p /usr/share/GeoIP
#ADD GeoLiteCity.dat /usr/share/GeoIP/GeoIPCity.dat




