FROM alpine as BUILD

WORKDIR /root

RUN apk --update --upgrade \
    add \
    git \
    less \
    openssh \
#     musl-dev gcc make g++ file alpine-sdk \
    make \
    cmake \
    python \
    python-dev \
    python3-dev \
    curl \
    wget \
    vim \
    && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*


RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget -q https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk && \
    apk add glibc-2.28-r0.apk && rm glibc-2.28-r0.apk

COPY ./mini_vimrc /root/.vimrc
RUN vim -E -s -u "/root/.vimrc" +PlugInstall +qall || :

RUN git clone --depth 1 https://github.com/thinca/vim-quickrun.git /root/.vim/plugged/vim-quickrun

# -----------------------------------------------------

FROM alpine

WORKDIR /root

COPY --from=BUILD /root/.vim /root/.vim
COPY --from=BUILD /root/.vimrc /root/.vimrc

RUN apk --update --upgrade add \
    python3-dev \
    git \
    make \
    cmake \
    curl \
    vim


ENTRYPOINT ["vim"]


