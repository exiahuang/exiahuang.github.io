---
categories: xycode
date: 2020/01/14 22:34:23
layout: post
tags:
- xycode
title: custom console in vscode
update_date: 2020/05/24 13:52:18

---

# Define console

Define console in [xycode](https://marketplace.visualstudio.com/items?itemName=ExiaHuang.xycode).

# config

```json
{
    "tasks": [
        {
            "label": "console: WSL",
            "description": "open WSL",
            "notShowProcess": true,
            "command": "cd ${workspaceFolder} && start wsl"
        },
        {
            "label": "console: cmd",
            "description": "open cmd",
            "notShowProcess": true,
            "command": "start cmd"
        },
        {
            "label": "console: Cmder",
            "description": "open Cmder",
            "notShowProcess": true,
            "command": "Cmder.exe /single ${workspaceFolder}"
        },
        {
            "label": "console: bash",
            "description": "open bash",
            "notShowProcess": true,
            "command": "cd ${workspaceFolder} && start bash"
        },
        {
            "label": "console: mintty.exe",
            "description": "open mintty.exe",
            "notShowProcess": true,
            "command": "start /b mintty.exe /bin/bash --login"
        },
        {
            "label": "windows: explorer",
            "description": "open explorer",
            "notShowProcess": true,
            "command": "start explorer ${workspaceFolder}"
        },
        {
            "label": "windows: open home directory",
            "description": "open home directory",
            "notShowProcess": true,
            "command": "start explorer ${HOME}"
        },
        {
            "label": "sublime",
            "description": "open sublime",
            "notShowProcess": true,
            "command": "\"C:\\Program Files\\Sublime Text 3\\sublime_text.exe\" \"${openFolderDailog:project_directory}\""
        },
        {
            "label": "sublime:open this workspace",
            "description": "open sublime",
            "notShowProcess": true,
            "command": "\"C:\\Program Files\\Sublime Text 3\\sublime_text.exe\" \"${workspaceFolder}\""
        }
    ],
    "variables": {
        "myproject_directory": {
            "label": "apex code snippt file",
            "value": ["${HOME}/.xycode"]
        }
    }
}
```

# define console

![xysfdx-open-wsl](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-open-wsl.gif)