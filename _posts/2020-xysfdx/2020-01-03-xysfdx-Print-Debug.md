---
categories: xysfdx
date: 2020/01/03 22:34:23
layout: post
tags:
- xysfdx
title: use xysfdx print debug
update_date: 2020/05/24 13:35:37

---

# print debug

-   `force:apex:log:tail`
-   `force:apex:log:tail:skiptraceflag`
-   `force:apex:log:tail:grep_debug_log`
-   `force:apex:log:tail:write_to_file`
-   `force:apex:log:tail:tee_to_file`

> for windows user, if you want to tee log to file, please change to `wsl`, `docker`, `bash` mode.

## usage example

run `force:apex:log:tail:grep_debug_log`

write a script, save and run it.

```java
string tempvar = 'Enter_your_name_here';
System.debug('Hello World!');
System.debug('My name is ' + tempvar);
```

view the log in termial.

![xysfdx-grep-debug-log](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xysfdx-grep-debug-log.gif)