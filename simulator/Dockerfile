FROM golang:1.21-bookworm

ARG LWN_SIMULATOR_VERSION=v1.0.3

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    git \
    make \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN git clone --depth 1 --branch ${LWN_SIMULATOR_VERSION} https://github.com/UniCT-ARSLab/LWN-Simulator.git . \
    && make install-dep

# Create non-root user
RUN useradd -r -s /sbin/nologin simulator \
    && chown -R simulator:simulator /app

USER simulator

EXPOSE 8000

CMD ["make", "run"]
