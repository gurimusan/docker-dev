From gurimusan/dev-base:latest

User root

RUN apk add --update --virtual build-deps \
    libtool \
    libx11-dev \
    libxpm-dev \
    libxt-dev \
    ncurses \
    ncurses-dev \
    ncurses-libs \
    ncurses-terminfo \
    python \
    python-dev \
    py-pip \
    python3 \
    python3-dev \
    ctags \
# Cleanup
    && rm -rf \
    /var/cache/* \
    /var/log/* \
    /var/tmp/* \
    && mkdir /var/cache/apk

ENV CMAKE_EXTRA_FLAGS=-DENABLE_JEMALLOC=OFF

WORKDIR /tmp

RUN git clone https://github.com/neovim/libtermkey.git && \
  cd libtermkey && \
  make && \
  make install && \
  cd ../ && rm -rf libtermkey

RUN git clone https://github.com/neovim/libvterm.git && \
  cd libvterm && \
  make && \
  make install && \
  cd ../ && rm -rf libvterm

RUN git clone https://github.com/neovim/unibilium.git && \
  cd unibilium && \
  make && \
  make install && \
  cd ../ && rm -rf unibilium

RUN  git clone https://github.com/neovim/neovim.git && \
  cd neovim && \
  git checkout v0.2.0 && \
  make CMAKE_BUILD_TYPE=Release && \
  make install && \
  cd ../ && rm -rf neovim

RUN pip install neovim
RUN pip3 install neovim

COPY init.vim       /home/gurimusan/.config/nvim/init.vim
COPY dein.toml      /home/gurimusan/.config/dein/dein.toml
COPY dein_lazy.toml /home/gurimusan/.config/dein/dein_lazy.toml

RUN chown gurimusan:gurimusan /home/gurimusan/.config/nvim/init.vim
RUN chown gurimusan:gurimusan /home/gurimusan/.config/dein/dein.toml
RUN chown gurimusan:gurimusan /home/gurimusan/.config/dein/dein_lazy.toml

USER gurimusan
WORKDIR /home/gurimusan

RUN curl https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh > installer.sh
RUN chmod +x ./installer.sh
RUN sh ./installer.sh /home/gurimusan/.config/deinrepo

# RUN nvim +":silent! call dein#install()" +qall
RUN nvim +PlugInstall +qall

RUN echo 'alias vim="nvim"' >> /home/gurimusan/.zshrc

CMD ["/usr/local/bin/nvim"]
