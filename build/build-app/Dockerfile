FROM devenv-image

WORKDIR /app

RUN git clone https://github.com/astrada/google-drive-ocamlfuse
WORKDIR /app/google-drive-ocamlfuse

# Deps & build for google-drive-ocamlfuse
RUN opam install ocamlfuse ocaml-systemd
#RUN eval $(opam config env)
RUN dune build @install

# Install the executable
RUN opam install -y google-drive-ocamlfuse

# Expose the default mount point
VOLUME /root/GoogleDrive

# Entry point to run the application
ENTRYPOINT ["opam", "config", "exec", "--", "app"]

# Default command when the container starts
CMD ["-label", "default", "/root/GoogleDrive"]

