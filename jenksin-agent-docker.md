
```bash
docker build  --build-arg JENKINS_REMOTING_TAG=4.13.2-1-jdk11 --tag techierishi/jenkins-agent-core:4.13.2-1-jdk11 .
docker push techierishi/jenkins-agent-core:jenkins-agent-core:4.13.2-1-jdk11 .
```


```Dockerfile
ARG JENKINS_REMOTING_TAG

FROM jenkins/inbound-agent:$JENKINS_REMOTING_TAG
ENV JENKINS_HOME=/home/jenkins

COPY build/install-esh.sh /tmp/build/install-esh.sh

WORKDIR ${JENKINS_HOME}

USER root

RUN set -ex && \
    apt-get update && \
    apt-get install -y \
        apt-transport-https \
        bash \
        bc \
        software-properties-common \
        ca-certificates \
        curl \
        expect \
        git \
        gpg \
        jq \
        make \
        python3 \
        python3-pip \
        python3-venv \
        shellcheck \
        gnupg \
        zip \
        && \
    pip3 install --upgrade \
        awscli \
        virtualenv \
        XlsxWriter==1.2.7 \
        Jinja2==2.9.6 \
        MarkupSafe==1.1.1 \
        && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    /tmp/build/install-esh.sh v0.3.1 && \
    rm -rf /tmp/build && \
    mkdir -p /usr/share/man/man1/ && \
    touch /usr/share/man/man1/sh.distrib.1.gz

# Python
RUN set -ex && \
    apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install git -y && \
    apt-get install -y \
        python3 \
        python3-pip \
        python3-venv \
        unixodbc-dev \
        dos2unix


RUN curl -fsSL https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | gpg --dearmor -o /usr/share/keyrings/adoptopenjdk-archive-keyring.gpg
RUN echo "deb [arch=arm64 signed-by=/usr/share/keyrings/adoptopenjdk-archive-keyring.gpg] https://adoptopenjdk.jfrog.io/adoptopenjdk/deb bullseye main" > /etc/apt/sources.list.d/adoptopenjdk.list
RUN apt-get update
RUN apt-get install -y adoptopenjdk-8-hotspot
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

#ENV JAVA_HOME /usr/lib/jvm/adoptopenjdk-8-hotspot-arm64

# Install maven
RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive \
    apt-get install -y maven \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# change /bin/sh to use bash, because lots of our scripts use bash features
RUN echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

USER jenkins

ENTRYPOINT ["jenkins-agent"]

```
