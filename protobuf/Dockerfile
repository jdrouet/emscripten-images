FROM trzeci/emscripten

ARG PROTOBUF_VERSION=v3.8.0

RUN apt-get update \
  && apt-get install -y autoconf automake libtool curl make g++ git unzip \
  && rm -rf /var/lib/apt/lists/*

RUN git clone \
  --branch ${PROTOBUF_VERSION} \
  --single-branch --depth 1 --recursive \
  https://github.com/protocolbuffers/protobuf.git /code/protobuf

WORKDIR /code/protobuf

RUN sh autogen.sh
RUN emconfigure ./configure
RUN emmake make
