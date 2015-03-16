FROM node:0.12-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    git autoconf automake ca-certificates build-essential libpcre3 libpcre3-dev; \
    git clone https://github.com/facebook/watchman.git; \
    cd watchman; ./autogen.sh; ./configure; make && make install; cd ~; \
    npm install -g \
    ember-cli   \
    bower       \
    phantomjs; \
    apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /watchman; \
    mkdir /home/ember /home/dist

EXPOSE 80 31609
WORKDIR /home/ember
ENTRYPOINT ["ember"]
CMD ["serve", "--port", "80", "--watcher", "polling"]

ONBUILD VOLUME ["/home/ember/dist"]
ONBUILD COPY . /home/ember
ONBUILD CMD ["build", "--output-path", "/home/dist", "--environment", "production"]
