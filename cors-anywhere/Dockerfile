FROM node:alpine
LABEL maintainer="ceshine@ceshine.net"

EXPOSE 80

RUN cd /opt && wget https://github.com/Rob--W/cors-anywhere/archive/master.zip && \
    unzip master.zip && rm master.zip
WORKDIR /opt/cors-anywhere-master

RUN npm install

ENV HOST 0.0.0.0
ENV PORT 80

CMD ["node", "server.js"]