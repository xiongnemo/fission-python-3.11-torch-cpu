ARG BUILDER_IMAGE=fission/builder
ARG PY_BASE_IMG=3.11-slim-bookworm

LABEL org.opencontainers.image.authors="nemo@anzupop.com"

FROM ${BUILDER_IMAGE}
FROM python:${PY_BASE_IMG}

COPY --from=0 /builder /builder
RUN apt update
RUN apt install -y python3-dev build-essential gcc bash

ADD defaultBuildCmd /usr/local/bin/build

EXPOSE 8001
