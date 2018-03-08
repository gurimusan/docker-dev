FROM gurimusan/nvim

USER root

RUN apk --no-cache add \
    wget \
    curl \
    curl-dev \
    git \
    grep \
    gmp-dev \
    libmcrypt-dev \
    freetype-dev \
    libxpm-dev \
    libwebp-dev \
    libjpeg-turbo-dev \
    libjpeg \
    bzip2-dev \
    openssl-dev \
    krb5-dev \
    libxml2-dev \
    build-base \
    tar \
    make \
    autoconf \
    bison \
    re2c \
    mysql-client \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

RUN mkdir -p /usr/src \
    && cd /usr/src \
    && git clone -b php-7.2.1 https://git.php.net/repository/php-src.git \
    && cd /usr/src/php-src \
    && ./buildconf \
    && ./configure \
        --enable-mbstring \
        --enable-zip \
        --enable-bcmath \
        --enable-pcntl \
        --enable-ftp \
        --enable-exif \
        --enable-calendar \
        --enable-sysvmsg \
        --enable-sysvsem \
        --enable-sysvshm \
        --enable-wddx \
        --with-curl \
        --with-mcrypt \
        --with-iconv \
        --with-gmp \
        --with-gd \
        --with-jpeg-dir=/usr \
        --with-webp-dir=/usr \
        --with-png-dir=/usr \
        --with-zlib-dir=/usr \
        --with-xpm-dir=/usr \
        --with-freetype-dir=/usr \
        --with-t1lib=/usr \
        --enable-gd-native-ttf \
        --enable-gd-jis-conv \
        --with-openssl \
        --with-mysql \
        --with-pdo-mysql \
        --with-zlib=/usr \
        --with-bz2=/usr \
        --with-kerberos=shared,/usr/lib \
        --disable-nls \
    && make \
    && make install \
    && cd ~ \
    && rm -fr /usr/src/php-src

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
    && /usr/bin/composer global require hirak/prestissimo

USER gurimusan
WORKDIR /home/gurimusan

CMD ["/bin/zsh"]
