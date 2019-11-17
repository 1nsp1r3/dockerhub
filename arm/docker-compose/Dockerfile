FROM alpine:latest

RUN apk update && \
  apk add gcc && \
  apk add make && \
  apk add python && \
  apk add python2-dev && \
  apk add musl-dev && \
  apk add libffi-dev && \
  apk add openssl-dev && \
  wget https://bootstrap.pypa.io/get-pip.py && \
  python get-pip.py && \
  rm get-pip.py && \
  pip install docker-compose

ENTRYPOINT ["/usr/bin/docker-compose"]

# docker build -t inspir3/arm-docker-compose ./
# docker login && docker push inspir3/arm-docker-compose
