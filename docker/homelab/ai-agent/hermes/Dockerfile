FROM nousresearch/hermes-agent:stable-desktop@sha256:87f24ae4be14980a3f2334bfe6516695253cb36dee5e9113b4348feea304c2ca


COPY --from=ghcr.io/jdx/mise:2026.11.8 /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}