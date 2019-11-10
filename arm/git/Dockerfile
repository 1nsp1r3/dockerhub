FROM alpine:latest

RUN apk update && \
  apk add git && \
  apk add openssh-client

ENTRYPOINT ["/usr/bin/git"]
