FROM openjdk:8

ARG ECLIPSE_DOWNLOAD_URL=http://mirror.switch.ch/eclipse/technology/epp/downloads/release/2018-09/R/eclipse-java-2018-09-linux-gtk-x86_64.tar.gz

ENV ECLIPSE_PACKAGE=eclipse-java.tar.gz
ENV USER_NAME user
ENV GID 1000
ENV UID 1000

ADD $ECLIPSE_DOWNLOAD_URL /tmp/$ECLIPSE_PACKAGE

RUN apt-get update && \
    apt-get install -y --no-install-recommends dbus dbus-x11 && \
    tar -xf /tmp/$ECLIPSE_PACKAGE -C /opt && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /var/lib/dpkg/info/* /tmp/*

RUN groupadd --gid $GID $USER_NAME && \
    useradd --uid $UID --gid $GID --create-home $USER_NAME

USER $USER_NAME

CMD ["/opt/eclipse/eclipse"]
