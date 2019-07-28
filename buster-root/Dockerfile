############################################################
# Dockerfile that contains SteamCMD
############################################################
FROM debian:buster-slim

LABEL maintainer="bert@lair.be"

ENV STEAMCMDDIR /home/steam/steamcmd

# Install, update & upgrade packages
# Create user for the server
# This also creates the home directory we later need
# Clean TMP, apt-get cache and other stuff to make the image smaller
# Create Directory for SteamCMD
# Download SteamCMD
# Extract and delete archive
RUN set -x \
    # Add i386 so we can install Wine downstream
    && dpkg --add-architecture i386 \
    && apt-get update \
    && apt-get install -y --no-install-recommends --no-install-suggests \
               lib32stdc++6 \
               lib32gcc1 \
               wget \
               ca-certificates \
    && groupadd steam \
    && useradd -m steam -g steam \
    && su steam -c \
	  "mkdir -p ${STEAMCMDDIR} \
		 && cd ${STEAMCMDDIR} \
		 && wget -qO- 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar zxf -" \
    && apt-get remove --purge -y \
	       wget \
    && apt-get clean autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

WORKDIR $STEAMCMDDIR

VOLUME $STEAMCMDDIR
