FROM sergeymakinen/yii2-php:base

LABEL maintainer "sergey@makinen.ru"

# PHP 5
RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y php-pear php5.6-cli php5.6-curl php5.6-gd php5.6-intl php5.6-mbstring php5.6-xml php5.6-zip php5.6-dev \
        php5.6-mysql php5.6-pgsql php5.6-sqlite3 \
    && pecl channel-update pecl.php.net \
    && rm -rf /var/lib/apt/lists/*

# Cubrid
RUN mkdir /root/tmp && pear config-set temp_dir /root/tmp \
    && pecl install cubrid pdo_cubrid \
    && echo 'extension=/usr/lib/php/20131226/cubrid.so' > /etc/php/5.6/mods-available/cubrid.ini \
    && echo 'extension=/usr/lib/php/20131226/pdo_cubrid.so' > /etc/php/5.6/mods-available/pdo_cubrid.ini \
    && phpenmod cubrid pdo_cubrid \
    && pear config-set temp_dir /tmp/pear/temp && rm -rf /root/tmp

# OCI for PHP 5
RUN apt-get update && apt-get install -y wget && mkdir /root/tmp && pear config-set temp_dir /root/tmp \
    && echo 'instantclient,/usr/lib/oracle/11.2/client64/lib' | pecl install oci8-2.0.12 \
    && cd /root/tmp && wget -q -O - https://pecl.php.net/get/PDO_OCI-1.0.tgz | tar ixz && ls -la && cd ./PDO_OCI-1.0 \
    && sed -i 's#libclntsh.$SHLIB_SUFFIX_NAME.10.1#libclntsh.$SHLIB_SUFFIX_NAME.11.2#g' ./config.m4 \
    && sed -i 's#PDO_OCI_VERSION=10.1#PDO_OCI_VERSION=11.2#g' ./config.m4 \
    && sed -i 's#10.2)#11.2)#g' ./config.m4 \
    && phpize \
    && sed -i 's#$prefix/include/php/ext#/usr/include/php/20131226/ext#g' ./configure \
    && ./configure \
    && sed -i 's#function_entry pdo_oci_functions#zend_function_entry pdo_oci_functions#g' ./pdo_oci.c \
    && C_INCLUDE_PATH=/usr/include/oracle/11.2/client64 make \
    && mv ./modules/pdo_oci.so /usr/lib/php/20131226 \
    && echo 'extension=/usr/lib/php/20131226/oci8.so' > /etc/php/5.6/mods-available/oci8.ini \
    && echo 'extension=/usr/lib/php/20131226/pdo_oci.so' > /etc/php/5.6/mods-available/pdo_oci.ini \
    && phpenmod oci8 pdo_oci \
    && pear config-set temp_dir /tmp/pear/temp && rm -rf /root/tmp \
    && rm -rf /var/lib/apt/lists/*
