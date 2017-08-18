Docker for gurimusan's development
==================================

    docker run -ti gurimusan/dev-base

Docker Images
--------------

- `dev-base`: alpine linux image.
- `nvim`: Neovim image.

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
