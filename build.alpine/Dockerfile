FROM node:alpine
MAINTAINER Andrey Kozhevnikov <a.kozhevnikov@omprussia.ru>

COPY ["appium", "/appium"]
COPY ["appium-aurora-driver", "/appium-aurora-driver"]

WORKDIR /appium

RUN set -ex ;\
    apk add --no-cache --virtual .gyp python make g++ ;\
    cd /appium-aurora-driver ;\
    npm install ;\
    npm run prepare ;\
    npm pack ;\
    mv appium-aurora-driver-*.tgz /appium-aurora-driver.tgz ;\
    cd /appium ;\
    rm -rf /appium-aurora-driver ;\
    npm install --production ;\
    npm install /appium-aurora-driver.tgz --save ;\
    npm install ;\
    npm run build ;\
    rm -f /appium-aurora-driver.tgz ;\
    apk del .gyp ;\
    npm cache clean --force ;\
    rm -rf /tmp/* /var/tmp/*

EXPOSE 4723

CMD ["/usr/local/bin/node", "."]