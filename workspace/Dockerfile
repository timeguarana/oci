FROM debian:stable-20240423-slim

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
    && pnpm completion bash > /usr/share/bash-completion/bash_completion

ADD https://www.postgresql.org/media/keys/ACCC4CF8.asc /tmp/postgresql.gpg.key
ADD postgresql.list /etc/apt/sources.list.d/postgresql.list
RUN gpg --dearmor -o /usr/share/keyrings/postgresql.gpg < /tmp/postgresql.gpg.key \
    && rm /tmp/postgresql.gpg.key \
    && apt-get update -qq \
    && apt-get install --no-install-recommends -y postgresql-client libpq-dev

RUN apt-get update -qq \
    && apt-get upgrade -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER dev

ENTRYPOINT [ "sleep", "infinity" ]
