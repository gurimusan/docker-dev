FROM gurimusan/nvim

USER root

RUN apk add --update \
    nodejs \
    yarn \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk \
    && yarn global add eslint@v4.19.0

USER gurimusan
WORKDIR /home/gurimusan

COPY dein.toml /tmp/dein.toml
RUN cat /tmp/dein.toml >> /home/gurimusan/.config/dein/dein.toml
RUN nvim +":silent! call dein#install()" +qall
RUN nvim +"UpdateRemotePlugins" +qall

CMD ["/bin/zsh"]
