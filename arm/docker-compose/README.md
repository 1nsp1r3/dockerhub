# Usage
```console
$ cat > ~/bin/docker-compose << EOF
#!/bin/sh

docker run \
  --volume /var/run/docker.sock:/var/run/docker.sock \
  --volume \$PWD/:\$PWD/ \
  --workdir \$PWD/ \
  -ti --rm \
  inspir3/arm-docker-compose "\$@"
EOF
$ chmod +x ~/bin/docker-compose
$ docker-compose --version
```

# Info
```console
alpine:latest (3.74 Mb)
 |
 |__ inspir3/arm-docker-compose:latest (167 Mb)

Total size: 170 Mb
```
