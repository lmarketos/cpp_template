FROM gcc:latest as GCC 

FROM ubuntu:23.10 as FINAL
LABEL Description="C++ Build Environment with support tools"

ENV HOME /root

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get -y --no-install-recommends install \
    build-essential \
    #clang \
    cmake \
    gdb \
    neovim \
    cppcheck \
    python3 \
    #clang-tidy \
    #clang-tools \
    #clang-format \
    #libgtest-dev \
    wget \
    git \
    libmpfr-dev \
    libgmp3-dev \
    libmpc-dev \
    ca-certificates
RUN wget http://ftp.gnu.org/gnu/gcc/gcc-13.2.0/gcc-13.2.0.tar.gz && \
    tar -xf gcc-13.2.0.tar.gz && \
    cd gcc-13.2.0 && \
    ./configure -v --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu --prefix=/usr/local/gcc-13.2.0 --enable-checking=release --enable-languages=c,c++ --disable-multilib --program-suffix=-13.2.0 && \
    make -j3 && \
    make install 
RUN mkdir clang && \
    git clone --depth=1 https://github.com/llvm/llvm-project.git && \
    cd llvm-project && \
    mkdir build && \
    cd build && \
    cmake -DLLVM_ENABLE_PROJECTS=clang -DCMAKE_BUILD_TYPE=Release -G "Unix Makefiles" ../llvm && \
    make && \
    make check-clang
ENV PATH="/llvm-project/build/bin:$PATH" 
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
