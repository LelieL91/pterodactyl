# SteamCMD Pterodactyl Game Image based on latest Debian stable by LelieL91
FROM        --platform=$TARGETOS/$TARGETARCH debian:bookworm-slim

LABEL       author="LelieL91" maintainer="admin@factotum.ovh"

LABEL       org.opencontainers.image.source="https://github.com/leliel91/pterodactyl"
LABEL       org.opencontainers.image.licenses=MIT

ENV         DEBIAN_FRONTEND=noninteractive

## Update base packages + Install dependencies + Clean temp files + Configure locale
RUN         apt update && apt -y upgrade && apt -y --no-install-recommends install \
            ca-certificates curl lib32gcc-s1 libicu-dev locales iproute2 tini \
            && apt -y autoremove \
            && apt clean \
            && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
            && echo "10.0.40.101 gamerarena.it" >> /etc/hosts \
            && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
            && dpkg-reconfigure --frontend=noninteractive locales \
            && update-locale LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8 \
            && useradd -m -d /home/container container   

# Configure user
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container --chmod=755 ./entrypoint.sh /entrypoint.sh
ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]