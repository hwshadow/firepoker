FROM node:6

# install global npm packages
RUN npm install -g \
    bower \
    grunt-cli@0.1.x

COPY ./docker/dev/docker-cmd.sh /usr/local/bin/docker-cmd.sh
RUN chown node:node /usr/local/bin/docker-cmd.sh && \
    chmod 0755 /usr/local/bin/docker-cmd.sh

WORKDIR /src

USER node

CMD [ "/bin/bash", "-c", "/usr/local/bin/docker-cmd.sh" ]
