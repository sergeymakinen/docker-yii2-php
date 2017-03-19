FROM sergeymakinen/yii2-php:base

LABEL maintainer "sergey@makinen.ru"

# PHP 7.1
RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y php-pear php7.1-cli php7.1-curl php7.1-gd php7.1-intl php7.1-mbstring php7.1-phpdbg php7.1-xml php7.1-zip php7.1-dev \
        php7.1-mysql php7.1-pgsql php7.1-sqlite3 \
    && pecl channel-update pecl.php.net \
    && rm -rf /var/lib/apt/lists/*

# OCI for PHP 7.1
RUN apt-get update && mkdir /root/tmp && pear config-set temp_dir /root/tmp \
    && echo 'instantclient,/usr/lib/oracle/11.2/client64/lib' | pecl install oci8 \
    && cd /root/tmp && apt-get source php7.1 && cd `find . -name 'php7.1-*' -type d` \
    && cd ./ext/pdo_oci && phpize && ./configure && C_INCLUDE_PATH=/usr/include/oracle/11.2/client64 make \
    && mv ./modules/pdo_oci.so /usr/lib/php/20160303 \
    && echo 'extension=/usr/lib/php/20160303/oci8.so' > /etc/php/7.1/mods-available/oci8.ini \
    && echo 'extension=/usr/lib/php/20160303/pdo_oci.so' > /etc/php/7.1/mods-available/pdo_oci.ini \
    && phpenmod oci8 pdo_oci \
    && pear config-set temp_dir /tmp/pear/temp && rm -rf /root/tmp \
    && rm -rf /var/lib/apt/lists/*

# sqlsrv
RUN apt-get update && apt-get install -y apt-transport-https wget unixodbc-dev \
    && wget -q https://packages.microsoft.com/keys/microsoft.asc -O - | apt-key add - \
    && wget -q -O - https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/microsoft.list \
    && apt-get update && apt-get upgrade -y && ACCEPT_EULA=Y apt-get install -y msodbcsql \
    && pecl install sqlsrv pdo_sqlsrv \
    && echo 'extension=/usr/lib/php/20160303/sqlsrv.so' > /etc/php/7.1/mods-available/sqlsrv.ini \
    && echo 'extension=/usr/lib/php/20160303/pdo_sqlsrv.so' > /etc/php/7.1/mods-available/pdo_sqlsrv.ini \
    && phpenmod sqlsrv pdo_sqlsrv \
    && rm -rf /var/lib/apt/lists/*
