FROM nousresearch/hermes-agent:stable-desktop@sha256:1343accb74013f38a22a11139ea7267bba9e8765d1236750c012f6b44a8ef127


COPY --from=ghcr.io/jdx/mise:2026.10.23 /usr/local/bin/mise /usr/local/bin/mise

ENV MISE_DATA_DIR=/mise/data \
    MISE_CONFIG_DIR=/mise/config \
    MISE_CACHE_DIR=/mise/cache \
    PATH=/mise/data/shims:${PATH}