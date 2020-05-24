---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: python in xycode
update_date: 2020/05/24 13:20:32

---

# Agenda

Use xycode and python.

# config

```json
{
    "tasks": [
        {
            "label": "python:run",
            "description": "run python file",
            "cwd": "${fileDirname}",
            "command": "python \"${file}\""
        },
        {
            "label": "python:version",
            "description": "print python version",
            "command": "python --version"
        }
    ],
    "variables": {},
    "onSaveEvents": [
        {
            "label": "format python code",
            "description": "format python code",
            "filetypes": [".py"],
            "inActive": false,
            "command": "yapf \"${file}\" --style \"google\" -i"
        },
        {
            "label": "run python file",
            "description": "run python file",
            "filetypes": [".py"],
            "inActive": true,
            "cwd": "${fileDirname}",
            "command": "python \"${file}\""
        }
    ]
}
```

> > please install yapf if you want to auto format python code.

# write hello world

```js
print('hello world, python');
```

After save the file, you can see the result.