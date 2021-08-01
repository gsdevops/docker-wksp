
## Some Dockerfile samples

  

* simple python
```dockerfile
FROM python:3.7

RUN pip install -U pip
COPY dist/OpsletsEc2-0.6.3.tar.gz /tmp
RUN pip install /tmp/OpsletsEc2-0.6.3.tar.gz
```


* utility packages (with args)
```dockerfile
FROM python:3.7

RUN mkdir -p /op/dist/

RUN curl -sL https://deb.nodesource.com/setup_12.x |   bash -
RUN apt-get update -qq && \
        apt-get install -y -qq curl wget vim net-tools zip unzip less openssl jq

RUN apt-get install -y nodejs
RUN npm install -g serverless@2.38.0

RUN npm install --save-dev serverless-wsgi serverless-python-requirements  serverless-domain-manager
RUN python3 -m venv  /zapper
RUN . /zapper/bin/activate && pip install -U -q --disable-pip-version-check zappa flask boto3 pyhocon pyyaml

RUN python3 -m venv  /gsdeployer

COPY dist/  /opt/dist/
RUN . /gsdeployer/bin/activate && pip install -U -q --disable-pip-version-check boto3 elasticsearch markupsafe ansible awscli pip  setuptools pychef requests pyhocon pyyaml
RUN . /gsdeployer/bin/activate &&  pip install -U --disable-pip-version-check /opt/dist/deployer-1.1.5.tar.gz
RUN . /gsdeployer/bin/activate &&  pip install -U --disable-pip-version-check /opt/dist/vpc_peerer-1.0.0.tar.gz


RUN mkdir -p /root/.kube
RUN mkdir -p /kubedeployer
WORKDIR /kubedeployer
RUN curl -s -o /kubedeployer/kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.18.9/2020-11-02/bin/linux/amd64/kubectl
RUN curl -s -o /kubedeployer/aws-iam-authenticator https://amazon-eks.s3.us-west-2.amazonaws.com/1.17.9/2020-08-04/bin/linux/amd64/aws-iam-authenticator
RUN chmod +x /kubedeployer/kubectl && mv  /kubedeployer/kubectl /usr/local/bin/
RUN chmod +x /kubedeployer/aws-iam-authenticator && mv /kubedeployer/aws-iam-authenticator /usr/local/bin/
ARG helmVer="v3.5.2"
RUN wget --quiet https://get.helm.sh/helm-$helmVer-linux-amd64.tar.gz && tar -xzvf helm-$helmVer-linux-amd64.tar.gz && mv linux-amd64/helm /usr/local/bin/

RUN mkdir -p /flyway
WORKDIR /flyway
RUN wget -qO- https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/6.5.2/flyway-commandline-6.5.2-linux-x64.tar.gz | tar xvz &&  ln -s `pwd`/flyway-6.5.2/flyway /usr/local/bin

```


* docker image for deployable app with custom overrides when deploying
```dockerfile
FROM node:12.18.3-buster

RUN apt update &&\
    apt install -y less  net-tools libsdl-pango-dev
RUN  apt-get update \
     && apt-get install -y wget gnupg ca-certificates \
     && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
     && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
     && apt-get update \
     && apt-get install -y google-chrome-stable \
     && rm -rf /var/lib/apt/lists/* \
     && wget --quiet https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh -O /usr/sbin/wait-for-it.sh \
     && chmod +x /usr/sbin/wait-for-it.sh
WORKDIR /app

ARG COMP
ARG BLDNUM
ENV BLDNUM ${BLDNUM:-bldnum_missing}
RUN echo "build is: ${BLDNUM}"
RUN test -n "$COMP" ||(echo "COMP  not set" && false)
COPY Common /app/Common/
COPY $COMP /app/$COMP/

RUN cd /app/Common/ && npm install

WORKDIR /app/$COMP

RUN npm config set python /usr/bin/python3.7
RUN npm install
RUN npm install -g node-gyp
RUN npm link ../Common/
RUN cd ../Common/node_modules/canvas && node-gyp rebuild

# this is to enable the html-pdf work
RUN sed -i '/openssl_conf/d' /etc/ssl/openssl.cnf

VOLUME /external_config
CMD rm src/app.setting.ts && ln -s /external_config/app.setting.ts src/app.setting.ts && \
    echo -e "Starting node:\n$(ls -lart src/app.setting.ts)\nContent:\n $(cat src/app.setting.ts)\n" && \
    npm start ; cat  /root/.npm/_logs/*
```