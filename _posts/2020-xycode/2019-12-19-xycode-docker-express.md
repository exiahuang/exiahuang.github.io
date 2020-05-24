---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: xycode express in docker
update_date: 2020/05/24 13:20:32

---

# xycode + docker + express

## config setup

download dockerfile

```sh
curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/docker/express/Dockerfile

curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/docker/express/docker-compose.yml
```

download xycode config for `docker-express`

```sh
cd ~/.xycode && curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/linux/xycode.docker-express.json

```

## start to develope express in docker

![xycode-docker-express](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-docker-express.gif)

## tips

add `docker` to your json file in `~/.xycode`,
then each task in this json config file will run in docker container.

```json
{
    "tasks": [
        yourtask...
    ],
    "variables": {
        "docker_image_name": {
            "label": "docker images name",
            "value": "node"
        }
    },
    "docker": {
        "dockerContainer": "${lowercaseWorkspaceName}_node_1",
        "dockerAppRoot": "/app/"
    }
}

```

> change `~/.xycode/xycode.docker-express.json` config file, define your command.