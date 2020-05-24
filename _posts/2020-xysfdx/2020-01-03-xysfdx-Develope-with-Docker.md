---
categories: xysfdx
date: 2020/01/03 22:34:23
layout: post
tags:
- xysfdx
title: xysfdx use docker mode to develope sfdx.
update_date: 2020/05/24 13:35:37

---

## use docker mode to develope sfdx

### vscode config

```json
{
    "xysfdx.shellMode": "docker",
    "xysfdx.shellPath": "",
    "xysfdx.dockerContainer": "${lowercaseWorkspaceName}_sfdx_1",
    "xysfdx.dockerAppRoot": "/app/sfdx"
}
```

### How to use docker ?

1. pull images : `docker: pull image exiasfdc/sfdx`

![xysfdx-docker-image](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-docker-image.gif)

2. create container : `docker: create sfdx container`

![xysfdx-docker-container](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-docker-container.gif)

3. use docker shell : `docker: attach docker shell`

![xysfdx-docker-bash](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-docker-bash.gif)

then , use the `xysfdx` to develope sfdx.

### attention

-   can not use `force:auth:web:login` or `force:auth:web:login:setdefaultusername`
-   can not use `force:project:create`
-   use `xy:auth:username:login` to auth