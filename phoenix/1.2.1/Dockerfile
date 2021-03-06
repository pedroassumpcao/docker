FROM pedroassumpcao/elixir:1.3.4

MAINTAINER Pedro Assumpcao <pedro.assumpcao@gmail.com>

ENV NODE_VERSION 5.4.0
ENV NPM_VERSION 2
ENV NPM_CONFIG_LOGLEVEL info

RUN set -ex && \
    for key in \
        9554F04D7259F04124DE6B476D5A82AC7E37093B \
        94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
        0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
        FD3A5288F042B6850C66B31F09FE44734EB7990E \
        71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
        DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    ; do \
      gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
    done

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
    curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" && \
    gpg --verify SHASUMS256.txt.asc && \
    grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - && \
    tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
    rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc && \
    npm install -g npm@$NPM_VERSION --prefix=/usr/local && \
    ln -s -f /usr/local/bin/npm /usr/bin/npm && \
    npm cache clear

RUN apt-get update && apt-get install -y postgresql-client-9.4

ENV PHOENIX_VERSION 1.2.1
ENV PORT 4000
ENV MIX_ENV prod

RUN mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new-$PHOENIX_VERSION.ez --force

CMD ["iex"]
