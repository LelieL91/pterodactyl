# SteamCMD Pterodactyl Installer Image based on latest Debian stable by LelieL91
FROM        --platform=$TARGETOS/$TARGETARCH debian:trixie-slim

LABEL       author="LelieL91" maintainer="admin@factotum.ovh"

LABEL       org.opencontainers.image.source="https://github.com/leliel91/pterodactyl"
LABEL       org.opencontainers.image.licenses=MIT

ENV         DEBIAN_FRONTEND=noninteractive

## Update base packages + Install dependencies + Clean temp files + Configure locale
RUN         apt update \
            && apt -y upgrade \
            && apt -y --no-install-recommends install ca-certificates curl lib32gcc-s1 locales git wget jq unzip xz-utils \
            && apt clean \
            && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
            && apt -y autoremove \
            && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
            && dpkg-reconfigure --frontend=noninteractive locales \
            && update-locale LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8
