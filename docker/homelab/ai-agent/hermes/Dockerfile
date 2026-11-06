FROM nousresearch/hermes-agent:stable-desktop@sha256:399ec6c0052a945b06b38de9d44d26b636237a60e97422d2d81f1c38b8d7c9fd


COPY --from=ghcr.io/jdx/mise:2026.10.23 /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}