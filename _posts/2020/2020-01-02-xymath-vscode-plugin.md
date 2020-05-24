---
date: 2020-01-02 17:20 +0900
layout: post
tags:
- vscode
- maths
title: xymath for vscode
update_date: 2020/05/24 14:38:40

---

# xymath README

- [visual studio marketplace](https://marketplace.visualstudio.com/items?itemName=ExiaHuang.xymath)

xymath is a wapper for `qalc` and `gnuplot` command.
You need to download `qalculate` and `gnuplot` if you want to use this plugin.

> What is Qalculate ? Qalculate! is a multi-purpose cross-platform desktop calculator. It is simple to use but provides power and versatility normally reserved for complicated math packages.

> What is gnuplot ? gnuplot is a portable command-line driven graphing utility.

## Features

-   math calculator.
-   autorun `.qalc` file after save.
-   autorun `.gp` `.gnuplot` file after save.

## config

## usage

### use Qalculate

create a `.qalc` file, and write some math formula, then save it.

example:
- exchange rates
- Calculus
- change Units

![xymath-qalc](https://github.com/exiahuang/xycode-doc/blob/gh-pages/images/xymath-qalc.gif?raw=true)

### use gnuplot

create a `.gp` file, and save it. 

example:
- plot sin(x)

![xymath-gnuplot](https://raw.githubusercontent.com/exiahuang/xycode-doc/gh-pages/images/xymath-gnuplot.gif)

## Requirements

-   Qalculate
-   gnuplot

## Extension Settings

```json
{
    "xymath.qalculate": "the path of qalculate, default : qalc",
    "xymath.gnuplot": "the path of gnuplot, default : gnuplot",
    "xymath.encoding": "if encoding error, you can set this value"
}
```

> Chinese user:
> "xymath.encoding" : "CP936",

> Japanese user:
> "xymath.encoding" : "CP932",

**Enjoy!**
