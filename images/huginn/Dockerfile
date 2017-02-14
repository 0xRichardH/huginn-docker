# NAME:     huginn/huginn
FROM registry.cn-hangzhou.aliyuncs.com/bymax/rails_base:2.3.2

ENV RAILS_ENV 'production'
ENV HUGINN_VERSION '1.0.1'

MAINTAINER Richard Hao "https://github.com/haoxilu"

RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 &&\
    tar xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2 -C /usr/local/share/ &&\
    sudo ln -sf /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin &&\
    phantomjs --version

RUN useradd deploy -s /bin/bash -m -U &&\
    mkdir -p /var/www/

ADD huginn /var/www/huginn

RUN cd /var/www/huginn &&\
    cp .env.example .env &&\
    bundle install --deployment &&\
    find /var/www/huginn/vendor/bundle -name tmp -type d -exec rm -rf {} + &&\
    chown -R deploy:deploy /var/www

RUN curl https://get.acme.sh | sh

WORKDIR /var/www/huginn

USER deploy
