FROM pedroassumpcao/erlang:19.1

MAINTAINER Pedro Assumpcao <pedro.assumpcao@gmail.com>

ENV ELIXIR_VERSION 1.3.4

RUN apt-get update && \
    apt-get install -y --no-install-recommends locales unzip && \
    export LANG=en_US.UTF-8 && \
    echo $LANG UTF-8 > /etc/locale.gen && \
    locale-gen && \
    update-locale LANG=$LANG && \
    rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

WORKDIR /elixir

RUN wget -q https://github.com/elixir-lang/elixir/releases/download/v$ELIXIR_VERSION/Precompiled.zip && \
    unzip Precompiled.zip && \
    rm -f Precompiled.zip && \
    ln -s /elixir/bin/elixirc /usr/local/bin/elixirc && \
    ln -s /elixir/bin/elixir /usr/local/bin/elixir && \
    ln -s /elixir/bin/mix /usr/local/bin/mix && \
    ln -s /elixir/bin/iex /usr/local/bin/iex

RUN /usr/local/bin/mix local.hex --force && \
    /usr/local/bin/mix local.rebar --force

WORKDIR /

CMD ["iex"]
