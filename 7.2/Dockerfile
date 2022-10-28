#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
FROM php:7.2-fpm

LABEL maintainer="JohnVu <vuvanthuyyamaha@gmail.com>"

# Set Arguments
ARG DEBIAN_FRONTEND=noninteractive

#
############################################################################
# Mandatory Software's Installed
############################################################################
#
# Mandatory Software's such as
# ( ctype / curl / date / dom / filter / fileinfo / ftp / hash / iconv /
#   json / mbstring / mysqlnd / libxml / openssl / pcre / pdo / pdo_sqlite /
#   posix / sqlite3 / readline / tokenizer / session / sodium / standard
#   xml / xmlreader / xmlwriter / zlib )
# are installed on the base image 'php:7.2-fpm' image.
# (https://github.com/docker-library/php/tree/master/7.2/bullseye/fpm)
#
RUN set -eux; \
    \
    # Update system package
    apt-get update -y; \
    apt-get upgrade -y; \
    \
    # Install system dependencies
    apt-get install -y --no-install-recommends \
        apt-utils \
        nano vim \
        htop cron \
        gnupg2 \
        wget \
        zip unzip \
        git; \
    # Cleanup: build deps and cache.
    rm -rf /var/lib/apt/lists/*; \
    \
    # Set tzdata
    dpkg-reconfigure tzdata; \
    \
    # Update pecl chanel
    pecl channel-update pecl.php.net; \
    rm -rf /tmp/pear ~/.pearrc; \
    \
    # Create log folder
    mkdir -p /var/log/php; chmod 777 /var/log/php;

#
#############################################################################
# Software's Installation
#############################################################################
#
RUN set -eux; \
    \
    savedAptMark="$(apt-mark showmanual | sort -u | sed ':a;N;$!ba;s/\n/ /g')"; \
    manualSave=""; \
    apt-get update -y; \
    \
    #--------------------------------------------------------------------------
    # Install the `zip` extension.
    # This extension requires:
    #     Packages: libzip-dev(libzip4)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libzip-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libzip\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure zip --with-libzip; \
    docker-php-ext-install -j$(nproc) zip; \
    \
    #--------------------------------------------------------------------------
    # OK Install the `bz2` extension.
    # This extension requires:
    #     Packages: libbz2-dev(libbz2-1.0 bzip2)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libbz2-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libbz2\|bzip2\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure bz2 --with-bz2; \
    docker-php-ext-install -j$(nproc) bz2; \
    \
    #--------------------------------------------------------------------------
    # Install the `bcmath` extension.
    #--------------------------------------------------------------------------
    docker-php-ext-configure bcmath --enable-bcmath; \
    docker-php-ext-install -j$(nproc) bcmath; \
    \
    #--------------------------------------------------------------------------
    # Install the `decimal` extension.
    # This extension requires:
    #     Packages: libmpdec-dev(libmpdec3)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libmpdec-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libmpdec\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install decimal; \
    docker-php-ext-enable decimal; \
    \
    #--------------------------------------------------------------------------
    # Install the `intl` (Internationalization) extension.
    # This extension requires:
    #     Packages: zlib1g-dev(zlib1g) libicu-dev(libicu63, icu-devtools)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends zlib1g-dev libicu-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(zlib1g\|libicu\|icu-devtools\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure intl --enable-intl; \
    docker-php-ext-install -j$(nproc) intl; \
    \
    #--------------------------------------------------------------------------
    # Install the `pcntl` (Process Control) extension.
    #--------------------------------------------------------------------------
    docker-php-ext-configure pcntl --enable-pcntl; \
    docker-php-ext-install -j$(nproc) pcntl; \
    \
    #--------------------------------------------------------------------------
    # Install the `mcrypt` extension.
    # This extension requires:
    #     Packages: libmcrypt-dev( libmcrypt4)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libmcrypt-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libmcrypt\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install mcrypt; \
    docker-php-ext-enable mcrypt; \
    \
    #--------------------------------------------------------------------------
    # Install the `xsl` extension.
    # This extension requires:
    #     Packages: libxslt1-dev(libxslt1.1)
    #     Extensions: libxml
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libxslt1-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libxslt1\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure xsl --with-xsl; \
    docker-php-ext-install -j$(nproc) xsl; \
    \
    #--------------------------------------------------------------------------
    # Install the `ldap` (Lightweight Directory Access Protocol) extension.
    # This extension requires:
    #     Packages: libldap2-dev(libldap-common libldap-2.4-2) libsasl2-dev(libsasl2-modules-db libsasl2-2)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libldap2-dev libsasl2-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libldap-common\|libldap\|libsasl2-modules-db\|libsasl2\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ --with-ldap-sasl; \
    docker-php-ext-install -j$(nproc) ldap; \
    \
    #--------------------------------------------------------------------------
    # Install the `imap` (IMAP, POP3 and NNTP) extension.
    # This extension requires:
    #     Packages: libc-client-dev(libc-client2007e) libkrb5-dev(libkrb5-3 libkrb5support0)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libc-client-dev libkrb5-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libc-client\|libkrb5\)\([a-z0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl; \
    docker-php-ext-install -j$(nproc) imap; \
    \
    #--------------------------------------------------------------------------
    # Install the `sockets` extension.
    #--------------------------------------------------------------------------
    docker-php-ext-configure sockets --enable-sockets; \
    docker-php-ext-install -j$(nproc) sockets; \
    \
    #--------------------------------------------------------------------------
    # Install the `soap` extension.
    # This extension requires:
    #     Packages: libxml2-dev(libxml2)
    #     Extensions: libxml
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libxml2-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libxml2\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure soap --enable-soap; \
    docker-php-ext-install -j$(nproc) soap; \
    \
    #--------------------------------------------------------------------------
    # Install the `opcache` extension.
    #--------------------------------------------------------------------------
    docker-php-ext-configure opcache --enable-opcache; \
    docker-php-ext-install -j$(nproc) opcache; \
    \
    #--------------------------------------------------------------------------
    # Install the `gd` extension.
    # This extension requires:
    #     Packages: libzip-dev(libzip4) libgd-dev(libgd3) libpng-dev(libpng16-16) libjpeg-dev
    #               libjpeg62-turbo-dev(libjpeg62-turbo) libfreetype6-dev(libfreetype6)
    #               libwebp-dev(libwebpdemux2 libwebpmux3 libwebp6) libxpm-dev(libxpm4)
    #               libavif-dev(libavif9)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libzip-dev libgd-dev \
        libpng-dev \
        libjpeg-dev libjpeg62-turbo-dev \
        libfreetype6-dev \
        libwebp-dev libxpm-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libzip\|libgd\|libpng\|libjpeg\|libjpeg62-turbo\|libfreetype6\|libwebpdemux\|libwebpmux\|libwebp\|libxpm\|libavif\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure gd --prefix=/usr --with-gd --with-jpeg-dir --with-png-dir --with-freetype-dir --with-webp-dir --with-xpm-dir; \
    docker-php-ext-install -j$(nproc) gd; \
    \
    #--------------------------------------------------------------------------
    # Install the `exif` extension.
    # This extension requires:
    #     Packages: libexif-dev(libexif12)
    #     Extensions: mbstring
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libexif-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libexif\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure exif --enable-exif; \
    docker-php-ext-install -j$(nproc) exif; \
    \
    #--------------------------------------------------------------------------
    # Install the `imagick` extension.
    # This extension requires:
    #     Packages: libmagickwand-dev(imagemagick-6-common libmagickcore-6 ...)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libmagickwand-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libmagickcore\|libmagickwand\|imagemagick-[0-9]-common\)\([a-z0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install imagick; \
    docker-php-ext-enable imagick; \
    true; \
    \
    #--------------------------------------------------------------------------
    # Install the `gnupg` extension. (1.5.1)
    # This extension requires:
    #     Packages: libgpgme-dev(libgpgme11)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libgpgme-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libgpgme\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install gnupg; \
    docker-php-ext-enable gnupg; \
    \
    #--------------------------------------------------------------------------
    # Install the `pdo_pgsql` with `pgsql` extension.
    # This extension requires:
    #     Packages: libpq-dev(libpq5)
    #     Extensions: pgsql
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libpq-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libpq\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure pgsql --with-pgsql; \
    docker-php-ext-install -j$(nproc) pgsql; \
    docker-php-ext-configure pdo_pgsql --with-pdo-pgsql=pgsql; \
    docker-php-ext-install -j$(nproc) pdo_pgsql; \
    \
    #--------------------------------------------------------------------------
    # Install the `mysqli/pdo_mysql` with `mysqlnd` extension.
    # This extension requires:
    #     Packages: mariadb-client(mariadb-common mariadb-client-core-10.3 mariadb-client-10.3 mariadb-client)
    #               default-mysql-client(mysql-common default-mysql-client)
    #     Extensions: mysqlnd
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends mariadb-client default-mysql-client; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(mariadb-common\|mariadb-client-core\|mariadb-client\|mysql-common\|default-mysql-client\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    docker-php-ext-configure mysqli --with-mysqli=mysqlnd; \
    docker-php-ext-install -j$(nproc) mysqli; \
    docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd; \
    docker-php-ext-install -j$(nproc) pdo_mysql; \
    \
    #--------------------------------------------------------------------------
    # Install the `mongodb` extension. (1.14.2)
    #--------------------------------------------------------------------------
    pecl install mongodb; \
    docker-php-ext-enable mongodb; \
    \
    #--------------------------------------------------------------------------
    # Install the `msgpack` extension.
    #--------------------------------------------------------------------------
    pecl install msgpack && \
    docker-php-ext-enable msgpack; \
    \
    #--------------------------------------------------------------------------
    # Install the `igbinary` extension. (handler Session)
    #--------------------------------------------------------------------------
    pecl install igbinary; \
    docker-php-ext-enable igbinary; \
    \
    #--------------------------------------------------------------------------
    # Install the `redis` extension.(5.3.7)
    # This extension requires:
    #     Packages: redis-tools(redis-tools)
    #     Extensions: msgpack json igbinary
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends redis-tools; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(redis-tools\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install --nobuild redis; \
    cd "$(pecl config-get temp_dir)/redis"; \
    docker-php-ext-configure "$(pecl config-get temp_dir)/redis" --enable-redis-msgpack --enable-redis-json --enable-redis-igbinary; \
    docker-php-ext-install -j$(nproc) "$(pecl config-get temp_dir)/redis"; \
    \
    #--------------------------------------------------------------------------
    # Install the `memcached` extension.(3.2.0)
    # This extension requires:
    #     Packages: libmemcached-dev(libmemcachedutil2 libmemcached11) zlib1g-dev(zlib1g) libsasl2-dev(libsasl2-modules-db libsasl2-2)
    #     Extensions: json session igbinary msgpack
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libmemcached-dev zlib1g-dev libsasl2-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libmemcachedutil\|libmemcached\|zlib1g\|libsasl2-modules-db\|libsasl2\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install --nobuild memcached; \
    cd "$(pecl config-get temp_dir)/memcached"; \
    docker-php-ext-configure "$(pecl config-get temp_dir)/memcached" --enable-memcached-session --enable-memcached-igbinary --enable-memcached-msgpack --enable-memcached-json; \
    docker-php-ext-install -j$(nproc) "$(pecl config-get temp_dir)/memcached"; \
    \
    #--------------------------------------------------------------------------
    # Install the `event` extension.(3.0.8)
    # This extension requires:
    #     Packages: libevent-dev(libevent-pthreads-2.1-7 libevent-openssl-2.1-7 libevent-extra-2.1-7 libevent-core-2.1-7 libevent-2.1-7)
    #               libssl-dev(libssl1.1)
    #     Extensions: openssl sockets
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libevent-dev libssl-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
            | grep '^\(libevent-core\|libevent-extra\|libevent-openssl\|libevent-pthreads\|libevent\|libssl\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install --nobuild event; \
    cd "$(pecl config-get temp_dir)/event"; \
    docker-php-ext-configure "$(pecl config-get temp_dir)/event" --enable-event-sockets --with-event-openssl; \
    docker-php-ext-install -j$(nproc) --ini-name zdocker-php-ext-event.ini "$(pecl config-get temp_dir)/event"; \
    \
    #--------------------------------------------------------------------------
    # Install the `yaml` extension.(2.2.2)
    # This extension requires:
    #     Packages: libyaml-dev(libyaml-0-2)
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libyaml-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libyaml\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install yaml; \
    docker-php-ext-enable yaml; \
    \
    #--------------------------------------------------------------------------
    # Install the `swoole` extension.(4.8.12)
    # This extension requires:
    #     Packages: libssl-dev(libssl1.1) libcurl4-openssl-dev(libcurl4 libcurl3-gnutls) libc-ares-dev(libc-ares2) libssh2-1-dev(libssh2-1)
    #     Extensions: sockets openssl http2 mysqlnd json curl cares
    #--------------------------------------------------------------------------
    apt-get install -y --no-install-recommends libssl-dev libcurl4-openssl-dev libc-ares-dev libssh2-1-dev; \
    manualSave="${manualSave} $(apt list --installed | awk -F'/' 'NR>0{print $1}' | grep '.*\(\([^v]\)\|\([^e]v\)\|\([^d]ev\)\|\([^-]dev\)\)$' \
        | grep '^\(libssl\|libcurl4\|libc-ares\|libssh2\)\([0-9.+-]*\)$' | sed ':a;N;$!ba;s/\n/ /g')"; \
    pecl install --nobuild swoole; \
    cd "$(pecl config-get temp_dir)/swoole"; \
    docker-php-ext-configure "$(pecl config-get temp_dir)/swoole" --enable-sockets --enable-openssl --enable-http2 --enable-mysqlnd --enable-swoole-json --enable-swoole-curl --enable-cares; \
    docker-php-ext-install -j$(nproc) "$(pecl config-get temp_dir)/swoole"; \
    \
    #--------------------------------------------------------------------------
    # Cleanup: build deps and cache.
    #--------------------------------------------------------------------------
    docker-php-source delete; \
    # reset apt-mark's "manual" list so that "purge --auto-remove" will remove all build dependencies
    apt-mark auto '.*' > /dev/null; \
    savedAptMark="${savedAptMark} ${manualSave}"; \
    [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark; \
    find /usr/local -type f -executable -exec ldd '{}' ';' \
        | awk '/=>/ { print $(NF-1) }' \
        | sort -u \
        | xargs -r dpkg-query --search \
        | cut -d: -f1 \
        | sort -u \
        | xargs -r apt-mark manual \
    ; \
    rm -rf /tmp/* /var/tmp/* /usr/src/* \
        /var/cache/apt/* /var/lib/apt/lists/* \
        /var/log/lastlog /var/log/faillog \
        /tmp/pear ~/.pearrc; \
    apt-get clean; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    \
    #--------------------------------------------------------------------------
    # Install composer
    #--------------------------------------------------------------------------
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    composer clear-cache;

# Copy php.ini/PHP-FPM settings to the container
COPY ./configs/php/php.ini-production ${PHP_INI_DIR}/php.ini
COPY ./configs/php/conf.d/* ${PHP_INI_DIR}/conf.d/
COPY ./configs/php-fpm/conf.d/* /usr/local/etc/php-fpm.d/

# Change default shell for root user.
RUN sed -i "s|root:/bin/ash|root:/bin/bash|i" /etc/passwd;
