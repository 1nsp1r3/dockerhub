```console
$ cat ~/bin/git
```

```sh
#!/bin/sh
docker run \
  -v $HOME/:$HOME/ \
  --user joe \
  -it --rm \
  inspir3/git $@
```

```console
$ chmod +x ~/bin/git
$ git --version
```

# Authentification
Create an user with same name/uid than your Linux user
```console
$ docker exec -it git adduser -D -G users -u 1001 -s /bin/sh joe
```

Update your image to save your configuration
```console
$ docker commit git inspir3/git
```
