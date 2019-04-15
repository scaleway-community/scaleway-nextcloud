## -*- docker-image-name: "scaleway/nextcloud:latest" -*-
ARG SCW_ARCH
FROM scaleway/ubuntu:${SCW_ARCH}-bionic

MAINTAINER Scaleway <opensource@scaleway.com> (@scaleway)


# Prepare rootfs for image-builder
RUN /usr/local/sbin/builder-enter

# Install packages
RUN apt-get update && apt-get install apt-transport-https \
  && apt-get -q update \
  && apt-get -y -q upgrade \
  && apt-get install -y -q \
     libffi-dev \
     libssl-dev \
     git \
     php7.[0-9]+ \
     mysql-server \
     pwgen \
     python \
     python-dev \
     apache2 \
     python-pip \
     jq \
     curl \
     unzip \
  && apt-get install -y -q \
     libapache2-mod-php \
     php-gd \
     php-json \
     php-curl \
     php-mysql \
     php-intl \
     php-imagick \
     php-zip \
     php-xml \
     php-mbstring \
     php-apcu \
     redis-server \
     php-ldap \
     php-smbclient \
  && apt-get clean

RUN wget https://download.nextcloud.com/server/releases/latest.zip \
    && unzip latest.zip -d /var/www/html/ \
    && rm latest.zip

# Patch rootfs
COPY ./overlay /

# Conf apache
RUN a2enmod rewrite

# Symlink doc readme to /root/
RUN ln -s /usr/share/doc/scaleway/nextcloud/README /root/README

# Enable services
RUN systemctl enable init-nextcloud init-mysql mysql

# Clean rootfs from image-builder
RUN /usr/local/sbin/builder-leave
