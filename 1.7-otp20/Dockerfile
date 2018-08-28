FROM omisegoimages/jenkins-slave-erlang:20
MAINTAINER Kridsada Thanabulpong <sirn@omise.co>

ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
ENV LANG=C.UTF-8

RUN apt-get update && \
    apt-get install -y \
        autoconf \
        autogen \
        build-essential \
        git \
        libtool \
        openssl

ENV ELIXIR_VERSION="v1.7.2"

RUN set -xe && \
    ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" && \
    ELIXIR_DOWNLOAD_SHA256="3258eca6b5caa5e98b67dd033f9eb1b0b7ecbdb7b0f07c111b704700962e64cc" && \
    curl -fsL -o elixir-src.tar.gz "${ELIXIR_DOWNLOAD_URL}" && \
    echo "${ELIXIR_DOWNLOAD_SHA256}  elixir-src.tar.gz" |sha256sum -c - && \
    mkdir -p /usr/local/src/elixir && \
    tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz && \
    rm elixir-src.tar.gz && \
    cd /usr/local/src/elixir && \
    make -j$(nproc) && \
    make install && \
    rm -rf /usr/local/src/elixir
