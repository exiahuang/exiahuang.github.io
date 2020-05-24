---
categories:
- Program
date: 2017-03-24 14:44:39
description: dos comment
layout: post
tags:
- windows
- IT
title: dos comment
update_date: 2020/05/23 23:56:51

---

# Dos BAT Comment

<div class="note primary">1. :: 注释内容（第一个冒号后也可以跟任何一个非字母数字的字符）
2. rem 注释内容（不能出现重定向符号和管道符号）
3. echo 注释内容（不能出现重定向符号和管道符号）〉nul
4. if not exist nul 注释内容（不能出现重定向符号和管道符号）
5. :注释内容（注释文本不能与已有标签重名）
6. %注释内容%（可以用作行间注释，不能出现重定向符号和管道符号）
7. goto 标签 注释内容（可以用作说明goto的条件和执行内容）
8. :标签 注释内容（可以用作标签下方段的执行内容）
</div>

### example

``` bash
echo on
rem this is a comment.
echo this is a comment.
:: this is a comment too.
echo this is a comment too.
```