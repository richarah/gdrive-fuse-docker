FROM sysenv-image AS opam-setup

WORKDIR /deps

# TODO: move more sensible
RUN apt-get install -y libcurl4-gnutls-dev libfuse-dev libgmp-dev libsqlite3-dev zlib1g-dev -y

RUN eval $(opam env --switch=default)
RUN opam init --disable-sandboxing
RUN eval $(opam config env)
RUN opam update -y
RUN opam upgrade -y
RUN opam install dune merlin ocaml-lsp-server odoc ocamlformat utop dune-release cryptokit extlib gapi-ocaml ocamlfuse gapi-ocaml ocamlfuse camlzip sqlite3 -y && eval $(opam config env)

FROM opam-setup

# Add dune to PATH
RUN PATH="$HOME/root/.opam/default/bin/dune:$PATH"

# tiny_httpd, gapi-ocaml, other pkgs forsaken by opam
WORKDIR /deps
RUN git clone https://github.com/c-cube/tiny_httpd
WORKDIR /deps/tiny_httpd
RUN export DUNE_CONFIG__GLOBAL_LOCK=disabled && eval $(opam env) && make -j$(nproc) && make install

WORKDIR /deps
RUN git clone https://github.com/astrada/gapi-ocaml
WORKDIR /deps/gapi-ocaml
RUN ./configure && make -j$(nproc) && make install
