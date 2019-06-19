FROM jdrouet/emscripten-protobuf:3.8.0

WORKDIR /root/protoc

RUN curl -L https://github.com/protocolbuffers/protobuf/releases/download/v3.8.0/protoc-3.8.0-linux-x86_64.zip --output protoc.zip \
  && unzip protoc.zip \
  && rm protoc.zip \
  && mv /root/protoc/bin/protoc /bin/protoc \
  && rm -rf /root/protoc

ARG ONNX_VERSION=v1.5.0

RUN git clone \
  --branch ${ONNX_VERSION} \
  --single-branch --depth 1 --recursive \
  https://github.com/onnx/onnx.git /code/onnx

WORKDIR /code/onnx

RUN emcmake cmake . \
  -DProtobuf_INCLUDE_DIR=/code/protobuf/src \
  -DProtobuf_LIBRARIES=/code/protobuf/src/.libs \
  -DProtobuf_LITE_LIBRARY=/code/protobuf/src/.libs \
  -DONNX_USE_LITE_PROTO=ON
RUN emmake make