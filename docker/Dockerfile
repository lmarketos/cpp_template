FROM ubuntu:22.04
LABEL Description="C++ Build Environment with support tools"

ENV HOME /root

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get -y --no-install-recommends install \
    build-essential \
    gcc \
    g++ \
    clang \
    cmake \
    gdb \
    neovim \
    cppcheck \
    python3 \
    clang-tidy \
    clang-format \
    gdb \
    libgtest-dev \
    wget \
    git \
    ca-certificates
RUN wget https://github.com/ninja-build/ninja/releases/latest/download/ninja-linux.zip && \
    mv ninja-linux.zip /usr/local/bin/ninja.gz && \
    gunzip /usr/local/bin/ninja.gz && \
    chmod a+x /usr/local/bin/ninja

 

