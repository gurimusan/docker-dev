FROM gurimusan/erlang

USER root

# elixir expects utf8.
ENV ELIXIR_VERSION="v1.7.2"

RUN set -xe \
  && ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/releases/download/${ELIXIR_VERSION}/Precompiled.zip" \
    && ELIXIR_DOWNLOAD_SHA512="e7ebdfcd301737967d0c04df50d3ba5b5a0663d2a2e2ac771cf61b9aa8d73a8f64dd9a408890ff0e2db4e48df8f94ff4d5fb7060f25592411e54910cdfc567a0" \
    && buildDeps=' \
        ca-certificates \
        curl \
        unzip \
    ' \
    && apk add --no-cache --virtual .build-deps $buildDeps \
    && curl -fSL -o elixir-precompiled.zip $ELIXIR_DOWNLOAD_URL \
    && echo "$ELIXIR_DOWNLOAD_SHA512  elixir-precompiled.zip" | sha512sum -c - \
    && unzip -d /usr/local elixir-precompiled.zip \
    && rm elixir-precompiled.zip \
    && apk del .build-deps

USER gurimusan
WORKDIR /home/gurimusan

COPY dein.toml /tmp/dein.toml
RUN cat /tmp/dein.toml >> /home/gurimusan/.config/dein/dein.toml
RUN nvim +":silent! call dein#install()" +qall
RUN nvim +"UpdateRemotePlugins" +qall

CMD ["iex"]
