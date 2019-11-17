FROM alpine:latest

RUN apk update && \
  apk add git && \
  apk add openssh-client

CMD ["/usr/bin/git"]

# docker build -t inspir3/arm-git ./
# docker login && docker push inspir3/arm-git
