FROM ubuntu:14.04


ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y python2.7 python-dev python-virtualenv build-essential libbz2-dev libfreetype6-dev libgdbm-dev libxft-dev
RUN apt-get install -y libjpeg-dev libldap2-dev libltdl-dev libmysqlclient-dev libreadline-dev libsasl2-dev libsqlite3-dev
RUN apt-get install -y libssl-dev libxslt1-dev ncurses-dev zlib1g-dev

RUN apt-get install -y redis-server mysql-server libmysqlclient-dev libmysqld-dev
RUN apt-get install -y supervisor nginx git

RUN apt-get install -y libcurl4-openssl-dev

RUN virtualenv /srv/selena_app
RUN chown -R www-data:www-data /srv/selena_app
RUN mkdir /etc/selena/
RUN chown www-data:www-data /etc/selena

USER www-data
RUN git clone http://github.com/allegro/selena /srv/selena_app/selena

WORKDIR /srv/selena_app/selena
RUN ../bin/pip install -e .
RUN ../bin/pip install gunicorn

ADD services.conf /etc/supervisor/conf.d/services.conf
ADD settings /etc/selena/settings
