FROM nousresearch/hermes-agent:stable-desktop@sha256:385725287c207b1517717167d8ac8631e5e7cd2d47a9954df18b6e95b6e5e78b


COPY --from=ghcr.io/jdx/mise:2026.10.23 /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}