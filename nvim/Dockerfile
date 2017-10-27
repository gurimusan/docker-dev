From gurimusan/dev-base:latest

User root

COPY init.vim       /home/gurimusan/.config/nvim/init.vim
COPY dein.toml      /home/gurimusan/.config/dein/dein.toml
COPY dein_lazy.toml /home/gurimusan/.config/dein/dein_lazy.toml

RUN apk add --update \
    python \
    python-dev \
    python3 \
    python3-dev \
    py-pip \
    py-setuptools \
    ctags \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

ENV CMAKE_EXTRA_FLAGS=-DENABLE_JEMALLOC=OFF

RUN apk add --update --virtual build-deps \
    gcc \
    g++ \
    make \
    cmake \
    alpine-sdk \
    build-base\
    m4 \
    linux-headers \
    automake \
    autoconf \
    libtool \
    libx11-dev \
    libxpm-dev \
    libxt-dev \
    ncurses \
    ncurses-dev \
    ncurses-libs \
    ncurses-terminfo \
    && cd /tmp \
    && git clone https://github.com/neovim/libtermkey.git \
    && cd libtermkey \
    && make \
    && make install \
    && cd ../ && rm -rf libtermkey \
    && git clone https://github.com/neovim/libvterm.git \
    && cd libvterm \
    && make \
    && make install \
    && cd ../ \
    && rm -rf libvterm \
    && git clone https://github.com/neovim/unibilium.git \
    && cd unibilium \
    && make \
    && make install \
    && cd ../ \
    && rm -rf unibilium \
    && git clone https://github.com/neovim/neovim.git \
    && cd neovim \
    && git checkout v0.2.0 \
    && make CMAKE_BUILD_TYPE=Release \
    && make install \
    && cd ../ \
    && rm -rf neovim \
    && pip install neovim  \
    && pip3 install neovim \
    && cd /home/gurimusan \
    && curl https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh > installer.sh \
    && chmod +x ./installer.sh \
    && sh ./installer.sh /home/gurimusan/.config/deinrepo \
    && rm -f installer.sh \
    && apk del build-deps \
    && rm -rf \
    /var/cache/* \
    /var/log/* \
    /var/tmp/* \
    && mkdir /var/cache/apk

RUN chown -R gurimusan:gurimusan /home/gurimusan/.config

USER gurimusan
WORKDIR /home/gurimusan

RUN nvim +":silent! call dein#install()" +qall
RUN nvim +"UpdateRemotePlugins" +qall

RUN echo 'alias vim="nvim"' >> /home/gurimusan/.zshrc

CMD ["/usr/local/bin/nvim"]
