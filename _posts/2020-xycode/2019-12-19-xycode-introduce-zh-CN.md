---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: xycode是vscode的轻量级命令执行器.
update_date: 2020/05/24 13:24:37

---

# xycode

[xycode](https://github.com/exiahuang/Xycode) 是 vscode 的轻量级命令执行器.

如果您想构建一个 vscode 扩展程序，也许您可 ​​ 以先使用`xycode`。

## 特征

- [x]  小于 100k.
- [x]  定义您的 vscode 扩展。
- [x]  只需要配置一次，是 Vscode 的 Task 扩展。
- [x]  Integrated with system command and work with vscode.
- [x]  支持 c 语言编程.
- [x]  支持 vbs.
- [x]  支持 dotnet core.
- [x]  支持 go language.
- [x]  支持 python.
- [x]  支持 ruby.
- [x]  支持 gradle language.
- [x]  支持 npm/nodejs/express/vue.
- [x]  支持 prettier, format source automatically.
- [x]  支持 Heroku development.
- [x]  支持 git command.
- [x]  支持 sfdx, 用于 Salesforce SFDX 开发的快速开发工具。
- [x]  支持 Wenyan 文言文編程語言.
- [x]  支持写博客 hexo/mkdoc blog.
- [ ]  TODO : jekyll .
- [ ]  TODO :  Docker development.
- [ ]  TODO : a calculator.


## 下载配置

### 在 vscode 中自动下载

执行 `xycode: download config`命令, 下载配置.

### 手动下载

从 github 中下载配置 [xycode-config](https://github.com/exiahuang/Xycode-config).
复制到 Home 目录( `~/.xycode` or `%USERPROFILE%/.xycode`)

## 自定义配置

### 创建 json 文件

在下面目录下创建配置
Windows user: `%USERPROFILE%/.xycode`
Linux/Mac user: `~/.xycode`

### json 数据结构

```json
{
    "tasks": [
        {
            "label": "label name, required",
            "description": "description, not required",
            "command": "your command, required",
            // cwd is not required
            "cwd": "path of current working directory",
            // filetypes is not required
            // "filetypes": [".py"],
            // if you not need the command , please set it true
            // "inActive": false,
            // show the message in termial, default show in channel.
            // "termial": { name?: string, shellPath?: string, shellArgs?: string[] | string };
            // before run the command, you can set some check.
            "beforeTriggers": [
                {
                    "type": "buildin",
                    "fn": "CheckFileExist",
                    "params": ["${project_directory}/${project_name}"]
                }
            ],
            // after ran the command, you can do something.
            "afterTriggers": [
                {
                    "type": "buildin",
                    "fn": "SwitchFolder",
                    "params": ["${project_directory}/${project_name}"]
                }
            ]
        }
    ],
    "variables": {
        "apex_template": {
            "label": "sfdc apex template",
            "description": "",
            "value": [
                "DefaultApexClass",
                "ApexException",
                "ApexUnitTest",
                "InboundEmailService"
            ]
        },
        "base_metadata": {
            "label": "default sfdc metadata",
            "description": "",
            "value": "ApexClass, ApexPage, ApexComponent, ApexTrigger"
        }
    }
}
```

### 预定义变量

-   \${HOME} - Home directory
-   \${file} - the current opened file
-   \${fileBasename} - the current opened file's basename
-   \${fileBasenameNoExtension} - the current opened file's basename with no file extension
-   \${workspaceFolder} - the path of the folder opened
-   \${workspaceFolderBasename} - the name of the folder opened in Sublime without any slashes (/)
-   \${fileDirname} - the current opened file's dirname
-   \${fileExtname} - the current opened file's extension
-   \${YYYYMMDD} - current date
-   \${YYYYMMDD_HHmm} - current datetime

### 预定义触发器

-   Mkdirs - make directory
-   SwitchFolder - switch project folder
-   OpenFile - open file
-   CheckFileExist - check file exist
-   Diff - diff file

### 用户交互命令

-   input - Custom Input String
-   select - Select List
-   multiselect - Multiple Select List
-   openFolderDailog - Folder Path Selector
-   singleFileDailog - File Path Selector
-   multiFilesDailog - Mutliple File Paths Selector

## 配置例子

### 例子 1: input

echo user input

```json
{
    "tasks": [
        {
            "label": "hello:echo:user-input",
            "description": "echo user input",
            "command": "echo ${input:project_directory}"
        }
    ],
    "variables": {}
}
```

if you want to set the default value, please define the variable:

```json
{
    "tasks": [
        {
            "label": "hello:echo:user-input",
            "description": "echo user input",
            "command": "echo ${input:project_directory}"
        }
    ],
    "variables": {
        "project_directory": {
            "label": "project directory",
            "value": "${HOME}/test-project"
        }
    }
}
```

### 例子 2: select

echo user select

```json
{
    "tasks": [
        {
            "label": "hello:echo:user-select",
            "description": "echo user select",
            "command": "echo ${select:dotnet_template}"
        }
    ],
    "variables": {
        "dotnet_template": {
            "label": "dotnet core template",
            "value": [
                "console",
                "classlib",
                "wpf",
                "wpflib",
                "wpfcustomcontrollib",
                "wpfusercontrollib",
                "winforms"
            ]
        }
    }
}
```

### 例子 3: multiselect

echo files path, you can use `separator` to control the result string.

```json
{
    "tasks": [
        {
            "label": "hello:echo:multiselect",
            "description": "echo user multiselect",
            "command": "echo ${multiselect:METADATA}"
        }
    ],
    "variables": {
        "METADATA": {
            "label": "sfdc metadata",
            "separator": ",",
            "value": [
                "ApexClass",
                "ApexComponent",
                "ApexPage",
                "ApexTestSuite",
                "ApexTrigger"
            ]
        }
    }
}
```

### 例子 4: openFolderDailog

echo directory path

```json
{
    "tasks": [
        {
            "label": "hello:echo:folder-path",
            "description": "echo directory",
            "command": "echo ${openFolderDailog:project_directory}"
        }
    ],
    "variables": {}
}
```

### 例子 5: singleFileDailog

single file dailog, you can use `filters` to control the file type.

```json
{
    "tasks": [
        {
            "label": "hello:echo:file-path",
            "description": "echo single file path",
            "command": "echo ${singleFileDailog:package_xml}"
        }
    ],
    "variables": {
        "package_xml": {
            "label": "sfdc package.xml path",
            "filters": { "package.xml": ["xml"] },
            "value": "./manifest/package.xml"
        }
    }
}
```

### 例子 6: multiFilesDailog

Mutliple File Paths Selector

-   use `filters` to control the file type.
-   use `separator` to control the result string.

```json
{
    "tasks": [
        {
            "label": "hello:echo:files-paths",
            "description": "echo files paths",
            "command": "echo ${multiFilesDailog:sfdcsourcesfiles}"
        }
    ],
    "variables": {
        "sfdcsourcesfiles": {
            "label": "sfdc sources files",
            "separator": ",",
            "value": ""
        }
    }
}
```

### 例子 7: run command in wsl

change the shellPath, you can run command in wsl/bash/powershell ... or other termial

```json
{
    "label": "run command in wsl",
    "termial": {
        "name": "xycode",
        "shellPath": "wsl.exe"
    },
    "command": "pwd"
}
```

### 例子 8: auto formatter and auto runner

After you save file in vscode,
It will use `yapf` to format code and run python code automatically.

```json
{
    "tasks": [],
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
            "inActive": false,
            "cwd": "${fileDirname}",
            "command": "python \"${file}\""
        }
    ]
}
```

### 例子 10: user prettier to format source code.

use `Prettier` to pretty code .

```json
{
    "tasks": [],
    "variables": {},
    "onSaveEvents": [
        {
            "label": "pretty code.",
            "description": "Prettier is an opinionated code formatter.",
            "filetypes": [".json", ".javascript", ".js", ".md", ".css", ".vue"],
            "inActive": false,
            "cwd": "${fileDirname}",
            "command": "prettier --write \"${file}\" --single-quote=true --end-of-line=lf --arrow-parens=always --tab-width=4"
        }
    ]
}
```

## 快捷键

快捷键: `ctrl+shift+i`

## 扩展程序设置

-   `xycode.maxBuffer`: The maxBuffer option specifies the largest number of bytes allowed on stdout or stderr.