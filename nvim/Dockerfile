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
    neovim \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

RUN apk add --update --virtual build-deps \
    gcc \
    g++ \
    make \
    cmake \
    && cd /home/gurimusan \
    && curl https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh > installer.sh \
    && chmod +x ./installer.sh \
    && sh ./installer.sh /home/gurimusan/.config/deinrepo \
    && rm -f installer.sh \
    && apk del build-deps \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

RUN chown -R gurimusan:gurimusan /home/gurimusan/.config

USER gurimusan
WORKDIR /home/gurimusan

RUN nvim +":silent! call dein#install()" +qall
RUN nvim +"UpdateRemotePlugins" +qall

RUN echo 'alias vim="nvim"' >> /home/gurimusan/.zshrc

CMD ["/usr/bin/nvim"]
