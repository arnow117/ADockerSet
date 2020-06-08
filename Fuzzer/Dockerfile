FROM arnow117/ubuntu_base:18.04

MAINTAINER arnow117 "arnow117@gmail.com"

# ENV LLVM_PATH /home/arnow117/Tools/LLVM
# # install LibFuzzer
# RUN apt-get update -y && apt-get install -y build-essential make cmake ninja-build
# RUN mkdir $LLVM_PATH
# WORKDIR $LLVM_PATH
# RUN mkdir $LLVM_PATH/src $LLVM_PATH/work
# RUN cd $LLVM_PATH/src && git clone --depth 1 http://llvm.org/git/llvm.git
# RUN cd $LLVM_PATH/src/llvm/tools && git clone --depth 1 http://llvm.org/git/clang.git
# RUN cd $LLVM_PATH/src/llvm/projects && git clone --depth 1 http://llvm.org/git/compiler-rt.git
# RUN cd $LLVM_PATH/src/llvm/projects && git clone --depth 1 http://llvm.org/git/libcxx.git
# RUN cd $LLVM_PATH/src/llvm/projects && git clone --depth 1 http://llvm.org/git/libcxxabi.git
# RUN cd $LLVM_PATH/src/llvm/projects && git clone --depth 1 http://llvm.org/git/lld.git
# WORKDIR $LLVM_PATH

# # install from clang src
# WORKDIR $LLVM_PATH
# RUN mkdir -p $LLVM_PATH/work/llvm && cd $LLVM_PATH/work/llvm
# RUN cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Release -DLIBCXX_ENABLE_SHARED=OFF  -DLIBCXX_ENABLE_STATIC_ABI_LIBRARY=ON $LLVM_PATH/src/llvm
# RUN ninja
# RUN rm -rf $LLVM_PATH/src
# ENV PATH="$LLVM_PATH/work/llvm/bin:$PATH"
# ADD env $LLVM_PATH/work/llvm

WORKDIR $WORK_PATH