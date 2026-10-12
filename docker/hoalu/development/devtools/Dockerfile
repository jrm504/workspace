FROM nousresearch/hermes-sandbox:desktop

COPY --from=ghcr.io/jdx/mise:2026.9.11 /usr/local/bin/mise /usr/local/bin/mise

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