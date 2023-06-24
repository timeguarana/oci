FROM debian:bookworm-20230612-slim

ENV LANG   C.UTF-8
ENV LC_ALL C.UTF-8
ENV VISUAL vim

RUN apt-get update -qq \
    && apt-get install --no-install-recommends -y \
        sudo bash-completion git vim gpg apt-transport-https ca-certificates openssh-client \
    && useradd -m dev -s /bin/bash \
    && echo "dev ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/dev \
    && chmod 0440 /etc/sudoers.d/dev

ADD https://deb.nodesource.com/gpgkey/nodesource.gpg.key /tmp/nodejs.gpg.key
ADD nodejs.list /etc/apt/sources.list.d/nodejs.list
RUN gpg --dearmor -o /usr/share/keyrings/nodejs.gpg < /tmp/nodejs.gpg.key \
    && rm /tmp/nodejs.gpg.key \
    && apt-get update -qq \
    && apt-get install --no-install-recommends -y nodejs \
    && corepack enable \
    && corepack prepare pnpm@latest --activate \
    && pnpm install-completion bash \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

USER dev

ENTRYPOINT [ "sleep", "infinity" ]
