---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: C Program in xycode
update_date: 2020/05/24 13:20:31

---

# Agenda

Use xycode and Gcc to develope c program.

# config

```json
{
    "tasks": [
        {
            "label": "make:version",
            "command": "make -v"
        },
        {
            "label": "make:clean",
            "command": "make clean"
        },
        {
            "label": "make:hello",
            "command": "make hello"
        },
        {
            "label": "make:all",
            "command": "make all"
        },
        {
            "label": "make:target",
            "command": "make ${input:make_target}"
        },
        {
            "label": "gcc:compile",
            "cwd": "${fileDirname}",
            "command": "gcc -o ${fileBasenameNoExtension} ${file}"
        },
        {
            "label": "gcc:compile_and_run",
            "cwd": "${fileDirname}",
            "command": "gcc -o ${fileBasenameNoExtension} ${file} && ${fileBasenameNoExtension}"
        }
    ],
    "variables": {},
    "onSaveEvents": [
        {
            "label": "compile and run c file",
            "description": "compile and run c file after save",
            "filetypes": [".c"],
            "inActive": false,
            "cwd": "${fileDirname}",
            "command": "gcc -o ${fileBasenameNoExtension} ${file} && ${fileBasenameNoExtension}"
        }
    ]
}
```

# write hello world

```c
#include <stdio.h>

int main(int argc, char *args[])
{
    printf("Hello, world!\n");
    return 0;
}
```

After save the file, you can see the result.