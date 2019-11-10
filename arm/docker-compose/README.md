```console
$ cat ~/bin/docker-compose
```

```sh
#!/bin/sh

docker run \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v "$(pwd)":"$(pwd)" \
  --workdir="$(pwd)" \
  -it --rm \
  inspir3/docker-compose $@
```

```console
$ chmod +x ~/bin/docker-compose
$ docker-compose --version
```
