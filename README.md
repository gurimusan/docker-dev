Docker for gurimusan's development
==================================

    docker run -ti gurimusan/dev-base

Docker Images
--------------

- `dev-base`: alpine linux image.
- `nvim`: Neovim image.
- `node`: node image.
- `octave`: octave image.

SSH Forwarding and Git
----------------------

    docker run -ti --rm \
      -v $SSH_AUTH_SOCK:$SSH_AUTH_SOCK \
      -e SSH_AUTH_SOCK=$SSH_AUTH_SOCK \
      gurimusan/dev-base:latest \
      zsh

Getting the Clipboard Working
-----------------------------

    docker run -ti --rm \
      -e DISPLAY=$DISPLAY \
      -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
      gurimusan/dev-base:latest zsh

See: https://stackoverflow.com/questions/25281992/alternatives-to-ssh-x11-forwarding-for-docker-containers

My launcher
------------

~/bin/dockerdev.sh

```sh
#!/bin/sh

h=/home/gurimusan

run_docker_container() {
    xhost +si:localuser:$USER > /dev/null
    docker run -ti \
        --rm \
        -u $UID:$GID \
        -e DISPLAY=$DISPLAY \
        -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
        -v $HOME/.gitconfig:$h/.gitconfig \
        -v $SSH_AUTH_SOCK:$SSH_AUTH_SOCK \
        -e SSH_AUTH_SOCK=$SSH_AUTH_SOCK \
        -v $2:$h/project \
        gurimusan/$1
}

workspacedir=`pwd`
if [ -n "$2" ]; then
    workspacedir=$2
fi

case $1 in
    octave)
        run_docker_container octave $workspacedir
        ;;
    node)
        run_docker_container node $workspacedir
        ;;
    nvim)
        run_docker_container nvim $workspacedir
        ;;
    *)
        run_docker_container dev-base $workspacedir
        ;;
esac
```
