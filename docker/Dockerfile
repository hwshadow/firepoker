FROM node:6 AS dev

# install global npm packages
RUN npm install -g \
    bower \
    grunt-cli@0.1.x

# Install PhantomJS
# Source: https://hub.docker.com/r/wernight/phantomjs/dockerfile
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        bzip2 \
        libfontconfig \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && mkdir /tmp/phantomjs \
 && curl -Ls https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 \
        | tar -xj --strip-components=1 -C /tmp/phantomjs \
 && mv /tmp/phantomjs/bin/phantomjs /usr/local/bin \
 && rm -rf /tmp/phantomjs
ENV KARMABROWSER="PhantomJS"

# container startup command
COPY ./docker/docker-cmd.sh /usr/local/bin/docker-cmd.sh
RUN chown node:node /usr/local/bin/docker-cmd.sh && \
    chmod 0755 /usr/local/bin/docker-cmd.sh

WORKDIR /src

USER node

CMD [ "/bin/bash", "-c", "/usr/local/bin/docker-cmd.sh" ]


FROM dev AS builder

USER root
COPY . /src
RUN chown -R node:node /src

USER node
RUN grunt build


FROM nginx:latest

COPY --from=builder ./src/dist /usr/share/nginx/html
