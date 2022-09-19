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
    clang-tools \
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
RUN git clone https://github.com/google/googletest.git && \
  cd googletest && \
  mkdir build && \
  cd build && \
  cmake .. && \
  make && \
  cp -r /googletest/googlemock/include/gmock /usr/local/include/gmock && \
  cp -r /googletest/googletest/include/gtest /usr/local/include/gtest && \
  mkdir /usr/local/lib/gtest; cp -r /googletest/build/lib/libgtest*.a /usr/local/lib/gtest/ && \
  mkdir /usr/local/lib/gmock; cp -r /googletest/build/lib/libgmock*.a /usr/local/lib/gmock/

 

