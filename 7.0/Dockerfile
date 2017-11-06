FROM sergeymakinen/yii2-php:base

LABEL maintainer="sergey@makinen.ru"

# PHP 7
RUN apt-get update && apt-get install -y php7.0-cli php7.0-curl php7.0-gd php7.0-intl php7.0-mbstring php7.0-phpdbg php7.0-xml php7.0-zip \
        php7.0-mysql php7.0-pgsql php7.0-sqlite3 \
    && rm -rf /var/lib/apt/lists/*

# OCI
RUN apt-get update && apt-get install -y php-pear php7.0-dev && pecl channel-update pecl.php.net \
    && mkdir $ORACLE_HOME/lib/sdk && ln -s $ORACLE/include/oracle/$ORACLE_INSTANTCLIENT_MAJOR/client64 $ORACLE_HOME/lib/sdk/include \
    && echo "instantclient,$ORACLE_HOME/lib" | pecl install oci8 \
    && rm -rf $ORACLE_HOME/lib/sdk \
    && TMP_DIR="$(mktemp -d)" && cd "$TMP_DIR" && apt-get source php7.0 \
    && cd $(find . -name 'php7.0-*' -type d)/ext/pdo_oci && phpize && ./configure && make \
    && mv modules/pdo_oci.so /usr/lib/php/20151012 && rm -rf "$TMP_DIR" \
    && echo 'extension=/usr/lib/php/20151012/oci8.so' > /etc/php/7.0/mods-available/oci8.ini \
    && echo 'extension=/usr/lib/php/20151012/pdo_oci.so' > /etc/php/7.0/mods-available/pdo_oci.ini \
    && phpenmod oci8 pdo_oci \
    && rm -rf /var/lib/apt/lists/* && apt-get purge -y --auto-remove php-pear php7.0-dev

# sqlsrv
RUN apt-get update && apt-get install -y php-pear php7.0-dev curl apt-transport-https \
        unixodbc-dev locales \
    && echo 'en_US.UTF-8 UTF-8' > /etc/locale.gen && locale-gen && pecl channel-update pecl.php.net \
    && curl -L https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl -L https://packages.microsoft.com/config/ubuntu/16.04/prod.list -o /etc/apt/sources.list.d/microsoft.list \
    && apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql \
    && pecl install sqlsrv pdo_sqlsrv \
    && echo 'extension=/usr/lib/php/20151012/sqlsrv.so' > /etc/php/7.0/mods-available/sqlsrv.ini \
    && echo 'extension=/usr/lib/php/20151012/pdo_sqlsrv.so' > /etc/php/7.0/mods-available/pdo_sqlsrv.ini \
    && phpenmod sqlsrv pdo_sqlsrv \
    && rm -rf /var/lib/apt/lists/* && apt-get purge -y --auto-remove php-pear php7.0-dev curl apt-transport-https
