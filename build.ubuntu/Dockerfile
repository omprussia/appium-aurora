FROM ubuntu:18.04
MAINTAINER Andrey Kozhevnikov <coderusinbox@gmail.com>

COPY ["appium", "/appium"]
COPY ["appium-aurora-driver", "/appium-aurora-driver"]

WORKDIR /appium

RUN set -ex ;\
    apt-get update ;\
    apt-get install -y curl gnupg2 ;\
    curl -sL https://deb.nodesource.com/setup_10.x | bash - ;\
    apt-get install -y nodejs git build-essential ;\
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
    apt-get purge -y curl gnupg2 build-essential ;\
    apt-get autoremove --purge -y ;\
    apt-get clean ;\
    npm cache clean --force ;\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 4723

CMD ["/usr/bin/node", "."]