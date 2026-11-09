# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.24-2026.11.0@sha256:58422480a299b16b6ea376c2167463206d430619ed02b40cd687c8bd6875519e
FROM ${BUILD_FROM}

# Install VLC
WORKDIR /usr/src

RUN \
    set -x \
    && apk add --no-cache \
        inotify-tools \
        nginx \
        pwgen \
        vlc \
    && addgroup vlc && adduser -D -G vlc vlc \
    && grep -q "dir == undefined ? 'file://~'" /usr/share/vlc/lua/http/js/controllers.js \
    && sed -i "s#dir == undefined ? 'file://~'#dir == undefined ? 'file:///media'#" \
           /usr/share/vlc/lua/http/js/controllers.js
        
WORKDIR /
COPY rootfs /

LABEL \
    org.opencontainers.image.title="Home Assistant App: VLC" \
    org.opencontainers.image.description="Turn your device into a Media Player with VLC" \
    org.opencontainers.image.source="https://github.com/home-assistant/app-vlc" \
    org.opencontainers.image.licenses="Apache License 2.0"
