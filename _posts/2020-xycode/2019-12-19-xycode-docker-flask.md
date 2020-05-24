---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: xycode flask in docker
update_date: 2020/05/24 13:20:32

---

# xycode + docker + flask

## config setup

download dockerfile

```sh
curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/docker/flask/Dockerfile

curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/docker/flask/docker-compose.yml
```

download xycode config for `docker-flask`

```sh
cd ~/.xycode && curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/linux/xycode.docker-flask.json

```

## start to develope flask in docker

![xycode-docker-flask](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-docker-flask.gif)

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
            "value": "flask"
        }
    },
    "docker": {
        "dockerContainer": "${lowercaseWorkspaceName}_flask_1",
        "dockerAppRoot": "/app/"
    }
}

```


> change `~/.xycode/xycode.docker-flask.json` config file, define your command.