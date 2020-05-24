---
categories:
- CmderForSublime
- develop
date: 2019/06/19 22:22:22
layout: post
tags:
- CmderForSublime
- Hexo
title: Cmder For Express and heroku
update_date: 2020/05/24 13:46:03

---

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/Zj3xVUN8rpw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


This is a guide about use [Cmder For Sublime](http://www.google.com) for Express + heroku + git development.

## Prepare

* install [nodejs](https://nodejs.org)
* install [git](https://git-scm.com/downloads)
* install [heroku cli](https://devcenter.heroku.com/articles/heroku-cli)

## express

### install
`express:install`

```
npm install express express-generator nodemon -g
```

### express project init

`express:init`


### npm install

```
npm install
```

### express run

`express:nodemon:run`
or
`express:nodemon:run:change_port`

http://localhost:3000

## heroku


![Heroku-Command](http://salesforcexytools.com/mystatic/media/CmderForSublime/CmderForSublime-003.png)

### heroku:login
heroku:login

### creates a new app
heroku:create

### git init

git:init

```bash
git init
```

![Git-Command](http://salesforcexytools.com/mystatic/media/CmderForSublime/CmderForSublime-001.png)

### Initialize a git repository in a new or existing directory
heroku:git:remote

### git:add:all
git:add:all

### push heroku project to master
heroku:git:push_heroku_to_master

### open the heroku app in a web browser
heroku:open

### tail heroku logs
heroku:logs:tail

### heroku:logout
heroku:logout


## git

### git init

git:init

```bash
git init
```

### git:remote:add:origin

git:remote:add:origin

### git:add and git:push

git:add

git:push:origin_to_master



### version control

#### change sorce

#### git:add and git:push

#### git:log
`git:log:pretty`
`git:log:pretty:graph`
`git:log:pretty:n`
`git:log:pretty:graph:n`

```java
[2019-06-20 00:29:07][info] ********************************************************************************
* c8ad857 [2019/06/19 23:32:28] init express project  (HEAD -> master, heroku/master) [exiahuang]
[2019-06-20 00:29:07][info] ********************************************************************************
```

![Git-Command](http://salesforcexytools.com/mystatic/media/CmderForSublime/CmderForSublime-002.png)