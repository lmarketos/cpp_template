FROM gcc:latest as GCC 

FROM ubuntu:23.10 as CLANG
ENV HOME /root/

RUN apt-get update && apt-get -y --no-install-recommends install \
    build-essential \
    cmake \
    clang \
    python3 \
    python3-pip \
    wget \
    git \
    libmpfr-dev \
    libgmp3-dev \
    libmpc-dev \
    ca-certificates

RUN git clone --depth 1 https://github.com/llvm/llvm-project.git
RUN cd llvm-project && cmake -S llvm -B build && cmake --build build

FROM lmarketos/clang_test as CLANG

FROM ubuntu:23.10 as FINAL
LABEL Description="C++ Build Environment with support tools"

ENV HOME /root

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get -y --no-install-recommends install \
    build-essential \
    cmake \
    gdb \
    neovim \
    cppcheck \
    python3 \
    python3-pip \
    wget \
    git \
    libmpfr-dev \
    libgmp3-dev \
    libmpc-dev \
    ca-certificates

COPY --from=GCC /usr/local/bin /usr/bin
COPY --from=GCC /usr/local/include /usr/include
COPY --from=GCC /usr/local/lib /usr/lib
COPY --from=GCC /usr/local/lib64 /usr/lib
COPY --from=GCC /usr/local/libexec /usr/libexec

#ENV PATH="/llvm-project/build/bin:$PATH" 
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

RUN pip install conan --break-system-packages && conan profile detect && chmod -R 777 /root

RUN mkdir /lib/llvm-16
COPY --from=CLANG /lib/llvm-16 /lib/llvm-16
COPY --from=CLANG /usr/lib/x86_64-linux-gnu/lib* /usr/lib/x86_64-linux-gnu
COPY --from=CLANG /llvm-project/build/bin/* /usr/local/bin/
RUN ln -s /lib/llvm-16/bin/clang /usr/bin/clang && \
  ln -s /lib/llvm-16/bin/clang++ /usr/bin/clang++
