---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: Nodejs in xycode
update_date: 2020/05/24 13:20:32

---

# Agenda

Use xycode and nodejs.

# config

```json
{
    "tasks": [
        {
            "label": "node:run",
            "description": "run node file",
            "cwd": "${fileDirname}",
            "command": "node \"${file}\""
        },
        {
            "label": "node:version",
            "description": "print node version",
            "command": "node -v"
        }
    ],
    "variables": {},
    "onSaveEvents": [
        {
            "label": "run js file",
            "description": "run javascript",
            "filetypes": [".js"],
            "inActive": false,
            "cwd": "${fileDirname}",
            "command": "node \"${file}\""
        }
    ]
}
```

# write hello world

```js
console.log('hello world, nodejs');
```

After save the file, you can see the result.