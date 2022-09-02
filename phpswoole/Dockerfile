FROM phpswoole/swoole:php8.0

RUN apt-get clean \
    && apt-get update \
    && apt-get -y install --no-install-recommends --assume-yes \
        libpng-dev \
        libzip-dev \
        libzip4 \
        libgmp-dev \
        zip \
        unzip \
        libssl-dev \
        git \
        net-tools \
        iputils-ping \
        vim \
        sudo \
        curl \
        dirmngr \
        apt-transport-https \
        lsb-release \
        ca-certificates \
        libjpeg-dev \
        libfreetype6-dev \
        supervisor \
        inotify-tools \
        procps \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install mysqli pdo_mysql gd pcntl zip bcmath gmp

# 安装inotify扩展
RUN pecl install inotify \
    && docker-php-ext-enable inotify

# 安装composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

WORKDIR /var/www

# docker login: nightcp
# docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t nightcp/phpswoole:tagname --push .