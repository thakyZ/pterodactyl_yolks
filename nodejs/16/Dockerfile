FROM        --platform=$TARGETOS/$TARGETARCH node:16-bullseye-slim

LABEL       author="Michael Parker & Neko Boi Nick" maintainer="950594+thakyZ@users.noreply.github.com"

RUN         apt update \
            && apt -y install ffmpeg iproute2 git sqlite3 libsqlite3-dev python3 python3-dev ca-certificates dnsutils tzdata zip tar curl build-essential libtool iputils-ping \
            && useradd -m -d /home/container container

ENV         PNPM_HOME="/root/.local/share/pnpm"
ENV         PATH="${PATH}:${PNPM_HOME}"

SHELL       ["/bin/bash", "-c"]

RUN         npm install npm@8.19.4 -g \
                                                           # PNPM_VERSION="8.7.5"
			&& curl -fsSL https://get.pnpm.io/install.sh | bash - \
            && SHELL=bash pnpm setup \
            && source /root/.bashrc

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
