## -*- docker-image-name: "fayoh/stm8-dev" -*-
FROM alpine:latest

LABEL Description="Tiny image with git and my personal gitconfig"
LABEL Maintainer="daniel.f.bengtsson@gmail.com"

RUN     apk add --no-cache git && \
        git clone --depth=1 https://github.com/fayoh/dotfiles.git ${HOME}/dotfiles && \
        mv ${HOME}/dotfiles/gitconfig ${HOME}/.gitconfig && \
        mv ${HOME}/dotfiles/gitignore_global ${HOME}/.gitignore_global && \
        rm -rf ${HOME}/dotfiles
WORKDIR /mnt/git
ENTRYPOINT ["git"]
