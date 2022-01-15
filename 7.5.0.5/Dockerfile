FROM openjdk:8-jre-slim-buster
LABEL maintainer "Serghei Cebotari <cebotariserghei@gmail.com>"

ENV VERSION=7.5.0.5

RUN apt-get update && apt-get install -y --no-install-recommends \
        curl \
        unzip \
        fontconfig \
        libfreetype6 \
	&& rm -rf /var/lib/apt/lists/*

RUN curl http://cdn.sencha.com/cmd/$VERSION/no-jre/SenchaCmd-$VERSION-linux-amd64.sh.zip -o /cmd-installer.zip && \
    unzip -p /cmd-installer.zip > /cmd-installer.run && \
    chmod +x /cmd-installer.run && \
    INSTALL4J_ADD_VM_PARAMS="-Djava.awt.headless=true" /cmd-installer.run -q -dir /opt/Sencha/Cmd/$VERSION && \
    rm /cmd-installer.run /cmd-installer.zip

# https://github.com/ariya/phantomjs/issues/15449
ENV OPENSSL_CONF="/etc/ssl/"

WORKDIR /app

ENV PATH="/opt/Sencha/Cmd:${PATH}"

ENTRYPOINT ["/opt/Sencha/Cmd/sencha"]
