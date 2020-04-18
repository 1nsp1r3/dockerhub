# Thanks to https://github.com/jmb12686/docker-filebeat/blob/master/Dockerfile

FROM golang:alpine as builder

RUN apk update                                                          && \
  apk add bash                                                          && \
  apk add git                                                           && \
  apk add make                                                          && \
  apk add gcc                                                           && \
  apk add libc-dev                                                      && \
  apk add binutils-gold                                                 && \
  mkdir -p /go/src/github.com/elastic/                              && \
  cd /go/src/github.com/elastic/                                    && \
  git clone --branch 7.7 --depth 1 https://github.com/elastic/beats.git && \
  cd /go/src/github.com/elastic/beats/filebeat                      && \
  make

FROM alpine:latest

COPY --from=builder /go/src/github.com/elastic/beats/filebeat/filebeat /usr/bin/filebeat

RUN mkdir -p /etc/filebeat/     && \
    mkdir -p /var/lib/filebeat/ && \
    chmod +x /usr/bin/filebeat

# --strict.perms=false Au lancement, filebeat ne va pas vérifier les droits unix de filebeat.yml
# -e                   Envoie les logs sur stdout/stderr
CMD ["/usr/bin/filebeat", "--strict.perms=false", "-e", "-c", "/etc/filebeat/filebeat.yml", "-path.data", "/var/lib/filebeat", "-path.config", "/etc/filebeat"]

# docker build --network host -t inspir3/arm-filebeat ./
# docker login && docker push inspir3/arm-filebeat
