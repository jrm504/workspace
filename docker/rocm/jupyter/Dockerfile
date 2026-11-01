# syntax=docker/dockerfile:1
# Check the latest index at https://pytorch.org/get-started/locally/ (select ROCm)
ARG TORCH_INDEX=https://download.pytorch.org/whl/rocm7.2
ARG GFX_TARGET=gfx1030

############################
# Stage 1: build venv + prune kernels
############################
FROM ubuntu:26.04 AS build
ARG TORCH_INDEX
ARG GFX_TARGET

RUN apt-get update && apt-get install -y --no-install-recommends \
      python3 python3-venv ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN python3 -m venv /opt/venv
ENV PATH=/opt/venv/bin:$PATH

RUN pip install --no-cache-dir torch torchvision torchaudio --index-url ${TORCH_INDEX}
RUN pip install --no-cache-dir jupyterlab numpy pandas matplotlib

# Keep only the kernels for GFX_TARGET (delete other gfx files in rocblas/hipblaslt)
RUN L=/opt/venv/lib/python3.12/site-packages/torch/lib; \
    for d in rocblas/library hipblaslt/library; do \
      if [ -d "$L/$d" ]; then \
        find "$L/$d" -type f -name '*gfx*' ! -name "*${GFX_TARGET}*" -delete; \
      fi; \
    done

############################
# Stage 2: runtime
############################
FROM ubuntu:26.04

RUN apt-get update && apt-get install -y --no-install-recommends \
      python3 ca-certificates libgomp1 libnuma1 \
      libelf1t64 libdrm2 libdrm-amdgpu1 \
    && rm -rf /var/lib/apt/lists/*

COPY --from=build /opt/venv /opt/venv
ENV PATH=/opt/venv/bin:$PATH

# If your card is gfx1031/gfx1032 (RX 6700/6600), uncomment the line below:
# ENV HSA_OVERRIDE_GFX_VERSION=10.3.0

WORKDIR /workspace
EXPOSE 8888
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--ServerApp.token="]