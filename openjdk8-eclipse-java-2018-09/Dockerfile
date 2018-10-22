FROM openjdk:8

ARG release_name=2018-09
ARG release_tag=R

ENV ECLIPSE_TAR=eclipse-java-${release_name}-linux-gtk-x86_64.tar.gz
ENV ECLIPSE_URL=http://mirror.switch.ch/eclipse/technology/epp/downloads/release/${release_name}/${release_tag}/${ECLIPSE_TAR}

# Use COPY because this will work with local files and remote URLs.
ADD $ECLIPSE_URL /tmp/

RUN apt-get update && \
    apt-get install -y --no-install-recommends dbus dbus-x11 && \
    tar -xf /tmp/$ECLIPSE_TAR -C /usr/local && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /var/lib/dpkg/info/* /tmp/*

RUN groupadd --gid 1000 user && \
    useradd --uid 1000 --gid 1000 --create-home user

USER user

# adding the export to .bashrc fixes a bug -> https://bugs.launchpad.net/ubuntu/+source/at-spi2-core/+bug/1193236
RUN echo 'export NO_AT_BRIDGE=1' >> /home/user/.bashrc

CMD /usr/local/eclipse/eclipse
