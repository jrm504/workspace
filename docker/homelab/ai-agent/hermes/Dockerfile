FROM nousresearch/hermes-agent:stable-desktop@sha256:04f7a36d125bc3ebdef090cd5cf0cccaa74699e5a1a77c2965a4db437f24bf13


COPY --from=ghcr.io/jdx/mise:2026.9.11 /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}