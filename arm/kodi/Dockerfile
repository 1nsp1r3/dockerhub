FROM alpine:latest

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" > /etc/apk/repositories && \
  echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
  apk update && \
  apk add libcdio && \
  apk add libnfs && \
  apk add kodi

CMD ["/usr/bin/kodi-standalone"]
