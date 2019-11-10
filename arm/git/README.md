```console
$ cat ~/bin/git
```

```sh
#!/bin/sh

docker run \
  --user joe \
  -v $HOME/:$HOME/ \
  --workdir=$PWD \
  -it --rm \
  inspir3/arm/git /usr/bin/git "$@"
```

```console
$ chmod +x ~/bin/git
$ git --version
```

# Authentification
Create an user with same name/uid than your Linux user
```console
$ docker run \
  -it \
  --name git \
  inspir3/arm/git \
  adduser -D -G users -u 1001 -s /bin/sh joe
```

Update your image to save your configuration
```console
$ docker commit git inspir3/arm/git
```
