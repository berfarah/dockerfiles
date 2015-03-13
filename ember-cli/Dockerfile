FROM node:0.12-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    git autoconf automake ca-certificates build-essential; \
    git clone https://github.com/facebook/watchman.git; \
    cd watchman; ./autogen.sh; ./configure; make; make install; cd; \
    npm install -g \
    ember-cli   \
    bower       \
    phantomjs; \
    apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /watchman; \
    mkdir /home/ember /home/dist

VOLUME ["/home/dist"]
WORKDIR /home/ember

ENTRYPOINT ["ember", "build", "--output-path", "/home/dist"]
CMD ["--watch", "--environment", "development"]

ONBUILD COPY . /home/ember
ONBUILD CMD ["--environment", "production"]
