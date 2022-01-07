# alpine-code-server-php

![GitHub](https://img.shields.io/github/license/martinussuherman/alpine-code-server-php) ![Docker Pulls](https://img.shields.io/docker/pulls/martinussuherman/alpine-code-server-php) ![Docker Stars](https://img.shields.io/docker/stars/martinussuherman/alpine-code-server-php)

[![From Alpine](https://img.shields.io/badge/FROM-martinussuherman/alpine--code--server-brightgreen.svg)](https://hub.docker.com/r/martinussuherman/alpine-code-server)

---

## What is this image for ?

This is an [Minimal Alpine Linux image with glibc](https://hub.docker.com/r/jeanblanchard/alpine-glibc) based image for [code-server](https://github.com/cdr/code-server/) bundled with PHP. It enables one to run [VS Code](https://code.visualstudio.com/) in the browser for developing PHP application.

---

## Why use this image?

*code-server* service on this container will run as `non-root` (`vscode`) user. This add an extra layer of security and are generally recommended for production environments. This container also allow mapping of the `user id` dan `group id` of the user running docker to `vscode` user and group, which will enable the use of more restrictive file permission.

---

## How to use this image?

### *Using docker run*

```bash
$ docker run --name code-server -v ~/path/on/host:/home/vscode -e TZ=Asia/Jakarta -e EUID=$(id -u) -e EGID=$(id -g) -p 8080:8080 martinussuherman/alpine-code-server-php
```
This will set the `timezone` to Asia/Jakarta (you will want to change it to your own timezone) and map the `user id` dan `group id` of the current user to `vscode` user and group.

### *Using docker-compose*

```yaml
version: '3'

services:
  code-server:
    image: martinussuherman/alpine-code-server-php
    environment:
      - TZ=Asia/Jakarta
      - EUID=1001
      - EGID=1001
    volumes:
      - ~/path/on/host:/home/vscode
    ports:
      - 8080:8080

```

*Note:*
1. You will want to change the value for `EUID` and `EGID` with your current user `user id` dan `group id`.
2. *code-server* config file will be saved to `~/path/on/host/.config/code-server/config.yaml`
