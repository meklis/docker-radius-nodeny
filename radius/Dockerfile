FROM ubuntu:18.04
LABEL maintainer="Max Boyar <max.boyar.a@gmail.com>"

ENV SERVER_VERSION=0.1.1

RUN apt update && apt -y upgrade
ADD https://github.com/meklis/all-ok-radius-server/releases/download/${SERVER_VERSION}/all-ok-radius-linux-amd64 /opt/all-ok-radius
COPY radius.conf.yml /opt/radius.conf.yml
RUN chmod +x /opt/all-ok-radius
ENTRYPOINT ["/opt/all-ok-radius", "-c", "/opt/radius.conf.yml"]
