---
categories: xycode
date: 2019/12/19 22:34:23
layout: post
tags:
- xycode
title: Salesforce CLI in xycode
update_date: 2020/05/24 13:28:02

---

# Agenda

Use xycode and Salesforce CLI to develope sfdc.

# config

Config for windows user: [xycode.sfdx.json](https://github.com/exiahuang/xycode-config/blob/master/windows/xycode.sfdx.json)

Config for linux  user: [xycode.sfdx.json](https://github.com/exiahuang/xycode-config/blob/master/linux/xycode.sfdx.json)

Config for mac user: [xycode.sfdx.json](https://github.com/exiahuang/xycode-config/blob/master/mac/xycode.sfdx.json)




# Solution

## Create a project

`force:project:create`

![xycode-sfdx-init-project](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-sfdx-init-project.gif)

## Authentication

`force:auth:web:login`

## Retrieve metadata

`force:source:retrieve:metadata`

![xycode-sfdx-retrieve-meta](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-sfdx-retrieve-meta.gif)

## Deploy metadata

`force:source:deploy:metadata`
`force:source:deploy:current_file`

## Diff metadata

`force:source:diff:metadata`

You can diff with any sfdc organization.

### diff source

![xycode-sfdx-diff-meta](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-sfdx-diff-meta.gif)



### diff profile

![xycode-sfdx-diff-profile-meta](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-sfdx-diff-profile-meta.gif)

# Useful Tips

## auto run apex anonymous code

auto run apex anonymous code after save .apex.

change the config: `~/.xycode/xycode.sfdx.json`
set `inActive` false as below.

```json
"onSaveEvents": [
    {
        "label": "auto run apex anonymous code.",
        "description": "run apex anonymous code after save.",
        "filetypes": [".apex"],
        "cwd": "${fileDirname}",
        "inActive": false,
        "command": "sfdx force:apex:execute --apexcodefile \"${file}\""
    }
]
```

also, you can write a command and run `.soql` after you save.

![xycode-sfdx-run-apex-anonymous](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xycode-sfdx-run-apex-anonymous.gif)

## pretty apex code

```json
    "onSaveEvents": [
        {
            "label": "pretty apex code.",
            "description": "use prettier-plugin-apex to format salesforce apex code. npm install --global prettier prettier-plugin-apex ",
            "filetypes": [".trigger", ".cls"],
            "cwd": "${fileDirname}",
            "inActive": true,
            "command": "prettier --parser=apex --write \"${file}\" --tab-width=4 --single-quote=true"
        },
        {
            "label": "pretty apex anonymous code.",
            "description": "pretty apex anonymous code",
            "filetypes": [".apex"],
            "cwd": "${fileDirname}",
            "inActive": true,
            "command": "prettier --parser=apex --write \"${file}\" --tab-width=4 --single-quote=true --apex-anonymous"
        },

    ]
```