FROM sergeymakinen/yii2-php:base

LABEL maintainer="sergey@makinen.ru"

# PHP 5.6
RUN apt-get update && apt-get install -y php5.6-cli php5.6-curl php5.6-gd php5.6-intl php5.6-mbstring php5.6-xml php5.6-zip \
        php5.6-mysql php5.6-pgsql php5.6-sqlite3 \
    && rm -rf /var/lib/apt/lists/*

# CUBRID
RUN apt-get update && apt-get install -y php-pear php5.6-dev && pecl channel-update pecl.php.net \
    && pecl install cubrid-9.3.0.0001 pdo_cubrid-9.3.0.0002 \
    && echo 'extension=/usr/lib/php/20131226/cubrid.so' > /etc/php/5.6/mods-available/cubrid.ini \
    && echo 'extension=/usr/lib/php/20131226/pdo_cubrid.so' > /etc/php/5.6/mods-available/pdo_cubrid.ini \
    && phpenmod cubrid pdo_cubrid \
    && rm -rf /var/lib/apt/lists/* && apt-get purge -y --auto-remove php-pear php5.6-dev

# OCI
RUN apt-get update && apt-get install -y php-pear php5.6-dev curl && pecl channel-update pecl.php.net \
    && mkdir $ORACLE_HOME/lib/sdk && ln -s $ORACLE/include/oracle/$ORACLE_INSTANTCLIENT_MAJOR/client64 $ORACLE_HOME/lib/sdk/include \
    && echo "instantclient,$ORACLE_HOME/lib" | pecl install oci8-2.0.12 \
    && rm -rf $ORACLE_HOME/lib/sdk \
    && TMP_DIR="$(mktemp -d)" && cd "$TMP_DIR" && curl -L https://pecl.php.net/get/PDO_OCI-1.0.tgz | tar ixz && cd PDO_OCI-1.0 \
    && sed -i "s#libclntsh.\$SHLIB_SUFFIX_NAME.10.1#libclntsh.\$SHLIB_SUFFIX_NAME.$ORACLE_INSTANTCLIENT_MAJOR#g" config.m4 \
    && sed -i "s#PDO_OCI_VERSION=10.1#PDO_OCI_VERSION=$ORACLE_INSTANTCLIENT_MAJOR#g" config.m4 \
    && sed -i "s#10.2)#$ORACLE_INSTANTCLIENT_MAJOR)#g" config.m4 \
    && phpize \
    && sed -i 's#$prefix/include/php/ext#/usr/include/php/20131226/ext#g' configure \
    && ./configure \
    && sed -i 's#function_entry pdo_oci_functions#zend_function_entry pdo_oci_functions#g' pdo_oci.c \
    && make \
    && mv modules/pdo_oci.so /usr/lib/php/20131226 && rm -rf "$TMP_DIR" \
    && echo 'extension=/usr/lib/php/20131226/oci8.so' > /etc/php/5.6/mods-available/oci8.ini \
    && echo 'extension=/usr/lib/php/20131226/pdo_oci.so' > /etc/php/5.6/mods-available/pdo_oci.ini \
    && phpenmod oci8 pdo_oci \
    && rm -rf /var/lib/apt/lists/* && apt-get purge -y --auto-remove php-pear php5.6-dev curl
