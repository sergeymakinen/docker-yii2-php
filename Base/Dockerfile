FROM sergeymakinen/oracle-instant-client:11.2

LABEL maintainer "sergey@makinen.ru"

# PHP
RUN apt-get update && apt-get install -y software-properties-common \
    && LC_ALL=C.UTF-8 add-apt-repository -s ppa:ondrej/php \
    && rm -rf /var/lib/apt/lists/* && apt-get purge -y --auto-remove software-properties-common

RUN mkdir /yii
VOLUME /yii
WORKDIR /yii
