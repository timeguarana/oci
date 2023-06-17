FROM debian:bookworm-20230612-slim

ENV LANG   C.UTF-8
ENV LC_ALL C.UTF-8
ENV VISUAL vim

RUN apt-get update -qq && \
    apt-get install --no-install-recommends -y sudo bash-completion git vim && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    useradd -m dev -s /bin/bash && \
    echo "dev ALL=(ALL) NOPASSWD: ALL" | EDITOR='tee -a' visudo

USER dev

ENTRYPOINT [ "sleep", "infinity" ]
