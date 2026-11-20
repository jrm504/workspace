FROM nousresearch/hermes-agent:stable-desktop@sha256:5f587d1c036e551f57f1c706c460b41a4f48de0c4763e5865343eafd3950a2bc


COPY --from=ghcr.io/jdx/mise:2026.11.8 /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}