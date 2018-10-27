# Thunderbird on Ubuntu

FROM ubuntu:18.10

MAINTAINER Reto Christen, CH-6300 Zug

ENV APP_PACKAGES thunderbird
ENV USER_NAME user
ENV GID 1000
ENV UID 1000

RUN apt-get update && \
    apt-get install -y --no-install-recommends $APP_PACKAGES dbus dbus-x11 && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /var/lib/dpkg/info/* /tmp/*

RUN groupadd --gid $GID $USER_NAME && \
    useradd --uid $UID --gid $GID --create-home $USER_NAME

USER $USER_NAME

CMD ["/usr/bin/thunderbird"]
