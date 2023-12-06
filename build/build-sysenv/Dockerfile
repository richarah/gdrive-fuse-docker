FROM ubuntu:18.04
# TODO: a way around all these eval $(opam config env)s

# System-wide reqs
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y \
    unzip \
    git \
    rsync \
    mercurial \
    darcs \
    curl \
    pkg-config \
    build-essential \
    emacs \
    sqlite \
    sqlite3 \
    zlib1g \
    libfuse-dev \
    libgmp-dev \
    libsqlite3-dev \
    zlib1g-dev \
    libcurl4-gnutls-dev
# RUN apt-get install -y libcurl4-openssl-dev zlib1g libgmp-dev m4 pkg-config zlib1g-dev curl git libsqlite3-ocaml-dev libfuse-dev emacs build-essential sqlite3 sqlite libnethttpd-ocaml-dev

# Get rid of any existing opam installation; may be deprecated
RUN apt-get remove opam -y

# Do not the apt package for opam - at time of writing, it has not been updated in years
WORKDIR /deps
RUN git clone https://github.com/ocaml/opam
WORKDIR /deps/opam
RUN make compiler -j$(nproc)
RUN ./configure --with-vendored-deps && make -j$(nproc) && make install
# Required ref. README
RUN opam init --disable-sandboxing
RUN eval $(opam config env)

#RUN opam install -y re base64 cmdliner cudf dose3
# ocamlgraph.2.1.0
# RUN opam install -y opam-file-format spdx_licenses opam-0install-cudf jsonm uutf sha swhid_core mccs

# TODO: make neater
# RUN eval $(opam config env) && ./configure --with-vendored-deps && make libinstall
