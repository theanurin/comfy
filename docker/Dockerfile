ARG BUILD__CONFIGURATION="undefined"

FROM alpine AS builder_undefined
ONBUILD RUN echo "ERROR: You must set BUILD__CONFIGURATION (cpu or gpucu126) via --build-arg"; exit 1

FROM python:3.12-slim AS builder_cpu
COPY ComfyUI.Data /data
ONBUILD RUN apt-get update \
    && apt-get install --yes build-essential git libgl1 libglib2.0-0 wget \
    && rm -rf /var/lib/apt/lists/*
ONBUILD COPY requirements.txt /usr/local/comfyui/
ONBUILD COPY requirements-cpu.txt /usr/local/comfyui/
ONBUILD RUN cd /usr/local/comfyui/ \
    && pip install --no-cache-dir --break-system-packages --requirement requirements-cpu.txt \
    && rm requirements.txt requirements-cpu.txt
ONBUILD COPY ComfyUI.Runtime /usr/local/comfyui
ONBUILD ENTRYPOINT [ \
    "python3", "/usr/local/comfyui/main.py", \
    "--cpu", \
    "--listen", "0.0.0.0", \
    "--base-directory", "/data/", \
    "--database-url", "sqlite:////data/user/comfyui.db" \
]

FROM pytorch/pytorch:2.11.0-cuda12.6-cudnn9-runtime AS builder_gpucu126
COPY ComfyUI.Data /data
ONBUILD RUN apt-get update \
    && apt-get install --yes build-essential git libgl1 libglib2.0-0 wget \
    && rm -rf /var/lib/apt/lists/*
ONBUILD COPY requirements.txt /usr/local/comfyui/
ONBUILD COPY requirements-gpucu126.txt /usr/local/comfyui/
ONBUILD RUN cd /usr/local/comfyui/ \
    && pip install --no-cache-dir --break-system-packages --requirement requirements-gpucu126.txt \
    && rm requirements.txt requirements-gpucu126.txt
ONBUILD COPY ComfyUI.Runtime /usr/local/comfyui
ONBUILD ENTRYPOINT [ \
    "python3", "/usr/local/comfyui/main.py", \
    "--listen", "0.0.0.0", \
    "--base-directory", "/data/", \
    "--database-url", "sqlite:////data/user/comfyui.db" \
]

FROM builder_${BUILD__CONFIGURATION} AS builder
VOLUME /data/user
CMD []
