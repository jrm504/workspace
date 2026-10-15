# syntax=docker/dockerfile:1
ARG ROCM_TAG=7.2.4-complete

############################
# Stage 1: build
############################
FROM rocm/dev-ubuntu-24.04:${ROCM_TAG} AS build

ARG GFX_TARGET=gfx1030

RUN apt-get update && apt-get install -y --no-install-recommends \
      git cmake ninja-build build-essential libcurl4-openssl-dev ca-certificates \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /src
RUN git clone --depth 1 https://github.com/ggml-org/llama.cpp .

RUN HIPCXX="$(hipconfig -l)/clang" HIP_PATH="$(hipconfig -R)" \
    cmake -S . -B build -G Ninja \
      -DGGML_HIP=ON \
      -DAMDGPU_TARGETS=${GFX_TARGET} \
      -DCMAKE_BUILD_TYPE=Release \
      -DLLAMA_CURL=ON \
      -DLLAMA_BUILD_TESTS=OFF \
    && cmake --build build --target llama-server -j"$(nproc)"

# Copy required files to /out
RUN mkdir -p /out/bin /out/lib /out/rocm/lib/rocblas /out/rocm/lib/hipblaslt \
    && cp build/bin/llama-server /out/bin/ \
    && cp -a build/bin/*.so* /out/lib/ 2>/dev/null || true

# ROCm libraries required by llama-server (and its .so files)
RUN export LD_LIBRARY_PATH=/src/build/bin:/opt/rocm/lib \
    && ldd /src/build/bin/llama-server | awk '/\/opt\/rocm/ {print $3}' \
       | sort -u | xargs -r -I{} cp -aL {} /out/rocm/lib/ \
    # Some libraries are loaded at runtime (dlopen), so ldd does not detect them
    && for p in libamd_comgr libhiprtc libhsa-runtime64 librocprofiler-register libroctx64 libhipblaslt libhipblas librocblas libamdhip64; do \
         cp -aL /opt/rocm/lib/${p}.so* /out/rocm/lib/ 2>/dev/null || true; \
       done

# Keep only kernels for GFX_TARGET
RUN if [ -d /opt/rocm/lib/rocblas/library ]; then \
      mkdir -p /out/rocm/lib/rocblas/library && \
      cp -a /opt/rocm/lib/rocblas/library/*${GFX_TARGET}* /out/rocm/lib/rocblas/library/ 2>/dev/null || true; \
      cp -a /opt/rocm/lib/rocblas/library/TensileManifest.txt /out/rocm/lib/rocblas/library/ 2>/dev/null || true; \
    fi \
    && if [ -d /opt/rocm/lib/hipblaslt/library ]; then \
      mkdir -p /out/rocm/lib/hipblaslt/library && \
      cp -a /opt/rocm/lib/hipblaslt/library/*${GFX_TARGET}* /out/rocm/lib/hipblaslt/library/ 2>/dev/null || true; \
      cp -a /opt/rocm/lib/hipblaslt/library/*.dat /out/rocm/lib/hipblaslt/library/ 2>/dev/null || true; \
    fi

############################
# Stage 2: runtime
############################
FROM ubuntu:24.04

RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates curl libcurl4t64 libssl3t64 libgomp1 libnuma1 \
      libelf1t64 libdrm2 libdrm-amdgpu1 \
    && rm -rf /var/lib/apt/lists/*

# llama-swap: fetch the latest version from GitHub Releases
RUN set -eux; \
    VER="$(curl -fsSL https://api.github.com/repos/mostlygeek/llama-swap/releases/latest \
           | grep -oP '"tag_name":\s*"v\K[^"]+')"; \
    echo "llama-swap version: ${VER}"; \
    curl -fsSL "https://github.com/mostlygeek/llama-swap/releases/download/v${VER}/llama-swap_${VER}_linux_amd64.tar.gz" \
      | tar -xz -C /usr/local/bin llama-swap; \
    chmod +x /usr/local/bin/llama-swap

COPY --from=build /out/bin/llama-server /usr/local/bin/llama-server
COPY --from=build /out/lib/   /usr/local/lib/llama/
COPY --from=build /out/rocm/  /opt/rocm/

ENV LD_LIBRARY_PATH=/usr/local/lib/llama:/opt/rocm/lib
ENV ROCM_PATH=/opt/rocm
# If the card is gfx1031/gfx1032 (RX 6700/6600), uncomment the line below:
# ENV HSA_OVERRIDE_GFX_VERSION=10.3.0

EXPOSE 8080
ENTRYPOINT ["llama-swap", "-config", "/models/llama-swap.yaml", "-listen", ":8080"]