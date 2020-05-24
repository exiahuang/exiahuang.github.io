---
categories:
- CmderForSublime
- develop
date: 2019/06/20 22:22:22
layout: post
tags:
- CmderForSublime
- Hexo
title: Cmder for Hexo Blog
update_date: 2020/05/24 13:46:03

---

### Video
<iframe width="560" height="315" src="https://www.youtube.com/embed/dv3FDA4J2Kg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## hexo command

| Lable | Command | Description |
| ---- | ---- | ---- |
| hexo:init | hexo init "workspaceFolder" |  |
| hexo:new | hexo new "title" |  |
| hexo:generate | hexo generate |  |
| hexo:publish | hexo publish file |  |
| hexo:server | hexo server --port hexo_port |  |
| hexo:clean | hexo clean |  |
| hexo:list | hexo list hexo_type |  |
| hexo:version | hexo version |  |
| hexo:debug | hexo --debug |  |
| hexo:deploy | echo "hexo deploy" |  |


![github setting](http://salesforcexytools.com/mystatic/media/hexo/Image002.png)

## config

this is the setting of `Cmder For Sublime`

```json
{
	"tasks" : [

	//////////////////////////Hexo Command Start/////////////////////////////////
		{
			"label" : "hexo:init",
			"encoding": "UTF-8",
			"command": "hexo init \"${input:workspaceFolder}\""
		},
		{
			"label" : "hexo:new",
			"encoding": "UTF-8",
			"command": "hexo new \"${input:title}\""
		},
		{
			"label" : "hexo:generate",
			"encoding": "UTF-8",
			"command": "hexo generate"
		},
		{
			"label" : "hexo:publish",
			"encoding": "UTF-8",
			"command": "hexo publish ${input:file}"
		},
		{
			"label" : "hexo:server",
			"encoding": "UTF-8",
			"os_termial": true,
			"command": "hexo server --port ${input:hexo_port}"
		},
		{
			"label" : "hexo:clean",
			"encoding": "UTF-8",
			"command": "hexo clean"
		},
		{
			"label" : "hexo:list",
			"encoding": "UTF-8",
			"command": "hexo list ${select:hexo_type}"
		},
		{
			"label" : "hexo:version",
			"encoding": "UTF-8",
			"command": "hexo version"
		},
		{
			"label" : "hexo:debug",
			"encoding": "UTF-8",
			"command": "hexo --debug"
		},
		{
			"label" : "hexo:deploy",
			"encoding": "UTF-8",
			"command": "hexo deploy"
		},

	//////////////////////////Hexo Command End/////////////////////////////////

	],
    "custom_env" : {
        "hexo_port" : 4000,
        "hexo_type" : ["page", "post", "route", "tag", "category"]
    }
}
```


## flow

* hexo:init
* hexo:new
* hexo:server
* New A github repository
* fix config
* hexo:publish
* hexo:generate


### about github setting

![github setting](http://salesforcexytools.com/mystatic/media/hexo/Image001.png)

### about `_config.yml`

Deploy To Github


```yml
url: http://salesforcexytools.com
root: /hexo-test

deploy:
  type: git
  repo: git@github.com:username/username.github.io.git
  branch: [master]

```

### Set

### Access URL

http://exiahuang.github.io/hexo-test

http://salesforcexytools.com/hexo-test/