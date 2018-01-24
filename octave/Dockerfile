FROM gurimusan/nvim

USER root

RUN apk update \
    && apk --no-cache add gnuplot fontconfig \
    && apk --no-cache add --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ --allow-untrusted octave font-ipa graphicsmagick graphicsmagick-dev \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

USER gurimusan
WORKDIR /home/gurimusan

COPY .octaverc /home/gurimusan/.octaverc

RUN echo "alias octave=\"octave --no-gui\"" >> /home/gurimusan/.zshrc

CMD ["/bin/zsh"]
