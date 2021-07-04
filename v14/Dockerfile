FROM node:14.15.3-alpine

MAINTAINER Nico Swiatecki

ENV NIGHTSCOUT_VERSION="14.2.1"

RUN apk --update add ca-certificates wget && \
    update-ca-certificates && \
    mkdir -p /opt/app

WORKDIR /opt/app
RUN mkdir -p /.temp && \
    wget "https://github.com/nightscout/cgm-remote-monitor/archive/$NIGHTSCOUT_VERSION.zip" -O /.temp/temp.zip && \
    unzip /.temp/temp.zip -d /.temp && \
    cp -r /.temp/cgm-remote-monitor-$NIGHTSCOUT_VERSION/. /opt/app && \
    rm -rf /.temp && \
    chown -R node:node /opt/app

USER node
RUN npm install && \
    npm run postinstall && \
    npm run env && \
    npm audit fix

EXPOSE 1337

CMD ["node", "server.js"]
