---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: xycodeはvscode の軽量コマンドエグゼキューター
update_date: 2020/05/24 13:24:23

---

# xycode

[xycode](https://github.com/exiahuang/Xycode) vscode の軽量コマンドエグゼキューターです.

vscode 拡張機能を作る前に、 `xycode`を使ってみてください。

## 機能

-   拡張のサイズは 100k 未満。
-   コマンドを統合して、vscode 拡張機能として、vscode で利用可能。
-   Salesforce SFDX 専用開発ツール。
-   Heroku 開発。
-   Git コマンド統合。
-   Docker 開発。
-   prettier 拡張、自動敵にコードをフォーマットする。
-   Python、Go、Ruby、C、C ++、Dotnet Core、Java などのプログラミング言語を統合。
-   hexo、jekyll、mkdoc などのブログを作成。
-   Wenyan 古典中国語プログラミング言語開発。
-   一度設定した後、グルバール再利用可能。


## コンフィグファイルのダウンロード方法

### vscode でダウンロードする

vscode で`xycode: download config`コマンドを実行して、既存のコンフィグファイルがダウンロード可能です。

### github 経由して、コンフィグファイルをダウンロードする

github [xycode-config](https://github.com/exiahuang/Xycode-config)　にアクセスして、
コンフィグファイルをダウンロードして、コンフィグファイルフォルダに保存してください。

> > コンフィグファイルフォルダとは？
> > Linux/Mac の場合 `~/.xycode`
> > windows の場合: `%USERPROFILE%/.xycode`

## コンフィグファイルのカスタマイズ

### コンフィグファイルを作成

コンフィグファイルフォルダに、json ファイルを作成してみてください。

### コンフィグファイルの構成

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
    },
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

### デフォールト変数

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

### デフォールトトリガー

-   Mkdirs - make directory
-   SwitchFolder - switch project folder
-   OpenFile - open file
-   CheckFileExist - check file exist
-   Diff - diff file

### ユーザーインタフェース

-   input - Custom Input String
-   select - Select List
-   multiselect - Multiple Select List
-   openFolderDailog - Folder Path Selector
-   singleFileDailog - File Path Selector
-   multiFilesDailog - Mutliple File Paths Selector

## 構成例

### 例 1: input

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

### 例 2: select

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

### 例 3: multiselect

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

### 例 4: openFolderDailog

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

### 例 5: singleFileDailog

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

### 例 6: multiFilesDailog

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

### 例 7: run command in wsl

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

### 例 8: auto formatter and auto runner

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

### 例 10: user prettier to format source code.

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

## ショートキー

ショートキー: `ctrl+shift+i`

## 拡張設定

-   `xycode.maxBuffer`: The maxBuffer option specifies the largest number of bytes allowed on stdout or stderr.