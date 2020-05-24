---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: xycode jekyll in docker
update_date: 2020/05/24 13:20:32

---

# xycode + docker + jekyll

## requirement

-   docker
-   vscode
-   [xycode](https://marketplace.visualstudio.com/items?itemName=ExiaHuang.xycode)

## config setup

download xycode config for `docker-jekyll`

```sh
cd ~/.xycode && curl -O https://raw.githubusercontent.com/exiahuang/xycode-config/master/linux/xycode.docker-jekyll.json

```

## start to develope jekyll in docker

1. new a jekyll project : use `docker:jekyll:new:project`
2. create a docker container : use `docker:jekyll:create container`
3. open jekyll server : use `docker:jekyll:serve`, open `http://localhost:4000/`
4. if you want to use commmand below, please install [jekyll/jekyll-compose](https://github.com/jekyll/jekyll-compose)
    - `docker:jekyll:new:page`
    - `docker:jekyll:new:post`
    - `docker:jekyll:new:draft`

> Add this line to your application's Gemfile: gem 'jekyll-compose', group: [:jekyll_plugins]
> And then execute: \$ bundle

New Project

![xycode-docker-jekyll-new-project](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-docker-jekyll-new-project.gif)

Open serve

![xycode-docker-jekyll-serve](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-docker-jekyll-serve.gif)

> change `~/.xycode/xycode.docker-jekyll.json` config file, define your command.