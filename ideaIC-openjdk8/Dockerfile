# IntelliJ IDEA

FROM openjdk:8

ENV APP_VERSION=2018.2.5
ENV APP_DOWNLOAD_URL=https://download-cf.jetbrains.com/idea/ideaIC-${APP_VERSION}.tar.gz
ENV APP_PACKAGE=ideaIC.tar.gz
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
    mkdir /home/user/IdeaProjects && \
    chown user:user /home/user/IdeaProjects

USER $USER_NAME

ENTRYPOINT ["/opt/idea-IC-182.4892.20/bin/idea.sh"]
