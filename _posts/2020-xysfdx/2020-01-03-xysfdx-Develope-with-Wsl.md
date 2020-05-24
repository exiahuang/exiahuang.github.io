---
categories: xysfdx
date: 2020/01/03 22:34:23
layout: post
tags:
- xysfdx
title: xysfdx Use WSL mode to develope sfdx.
update_date: 2020/05/24 13:35:37

---

## Use WSL mode to develope sfdx

use wsl/git bash/Msys2 bash to develope sfdx.

### Open cmd/wsl/bash

![xysfdx-open-wsl.png](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-open-wsl.png)

![xysfdx-open-wsl](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-open-wsl.gif)

### use wsl

open `wslmode`

```json
{
    "xysfdx.shellMode": "wsl",
    "xysfdx.shellPath": "C:\\Windows\\System32\\bash.exe"
}
```

### use msys2 bash

```json
{
    "xysfdx.shellMode": "bash",
    "xysfdx.shellPath": "C:\\msys64\\usr\\bin\\bash.exe"
}
```

### use git bash

```json
{
    "xysfdx.shellMode": "bash",
    "xysfdx.shellPath": "C:\\Program Files\\Git\\usr\\bin\\bash.exe"
}
```