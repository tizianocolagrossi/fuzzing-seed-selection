FROM ubuntu:latest

# Install prerequesites
RUN export DEBIAN_FRONTEND=noninteractive &&    \
    apt update &&                               \
    apt install -y git build-essential cmake    \
        libboost-container-dev libz-dev python3

# Add OptiMin source
ADD CMakeLists.txt /optimin/
ADD src /optimin/src

# Build OptiMin
RUN mkdir -p /optimin/build
RUN cd /optimin/build &&        \
    cmake .. &&                 \
    make -j &&                  \
    make install

# Build EvalMaxSAT
RUN git clone https://github.com/FlorentAvellaneda/EvalMaxSAT
RUN cd EvalMaxSAT && git checkout 440bf90edf88f6ab940934129e3c5b3b93764295  && cd ..
RUN mkdir -p EvalMaxSAT/build
RUN cd EvalMaxSAT/build &&      \
    cmake .. &&                 \
    make -j &&                  \
    make install

# Add OptiMin wrapper
ADD optimin.py /optimin/
ENTRYPOINT ["/optimin/optimin.py"]
