# Eclipse IDE for Java Developers

FROM openjdk:8

ENV APP_VERSION=2018-09
ENV APP_DOWNLOAD_URL=http://ftp-stud.fht-esslingen.de/pub/Mirrors/eclipse/technology/epp/downloads/release/${APP_VERSION}/R/eclipse-java-${APP_VERSION}-linux-gtk-x86_64.tar.gz
ENV APP_PACKAGE=app.tar.gz
ENV USER_NAME user
ENV GID 1000
ENV UID 1000

ADD $APP_DOWNLOAD_URL /tmp/$APP_PACKAGE

RUN apt-get update && \
    apt-get install -y --no-install-recommends dbus dbus-x11 && \
    tar -xf /tmp/$APP_PACKAGE -C /opt && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /var/lib/dpkg/info/* /tmp/*

RUN groupadd --gid $GID $USER_NAME && \
    useradd --uid $UID --gid $GID --create-home $USER_NAME && \
    mkdir /home/user/eclipse-workspace && \
    chown user:user /home/user/eclipse-workspace

USER $USER_NAME

ENTRYPOINT ["/opt/eclipse/eclipse"]
