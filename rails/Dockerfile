FROM phusion/passenger-ruby22:latest
MAINTAINER Bernardo Farah <hi@bernardo.me>

## Expose log files and app files
VOLUME ["/home/app", "/var/log/nginx"]
WORKDIR /home/app
CMD ["/sbin/my_init"]

ADD /runit/app /etc/service/app

ONBUILD COPY ./app.conf /etc/nginx/sites-enabled/app.conf

ONBUILD COPY Gemfile Gemfile.lock /home/app/
ONBUILD RUN rm /etc/nginx/sites-enabled/default; \
            rm -f /etc/service/nginx/down; \
            bundle install

ONBUILD COPY . /home/app/
