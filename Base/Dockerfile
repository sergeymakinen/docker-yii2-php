FROM sergeymakinen/oracle-instant-client:11.2

LABEL maintainer "sergey@makinen.ru"

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# PHP
RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository -s ppa:ondrej/php \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /yii
VOLUME /yii
WORKDIR /yii

CMD tail -f /dev/null
