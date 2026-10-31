FROM nousresearch/hermes-sandbox:v0.21.7-desktop@sha256:c7d8607d076f26a64e0bd6828f74e1764af43fe3281368188459bb693bfa7567

COPY --from=ghcr.io/jdx/mise:2026.10.25@sha256:91417f41840316b7c5da6854bef393eccea4546ae70f8baf0803e0e94287b68d /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}

COPY certs/internal-rootca.crt /usr/local/share/ca-certificates/internal-rootca.crt
RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates nano fish \
    && update-ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Ensure runtimes without a system store trust the internal CA.
ENV SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt \
    REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt \
    NODE_EXTRA_CA_CERTS=/usr/local/share/ca-certificates/internal-rootca.crt

WORKDIR /opt/workspace