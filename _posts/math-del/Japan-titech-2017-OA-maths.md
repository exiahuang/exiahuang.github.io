---
title: one examination questions from Tokyo Institute of Technology
date: 2018-09-28 22:17:53
tags:
typora-copy-images-to: maths/images
typora-root-url: ./
mathjax: true
---

# Overview

* I  will talk about one examination questions from Tokyo Institute of Technology (東京工業大学) OA exam.
* Extra Analysis : About Floyd, DP( Dynamic programming)



# 試験問題

> Tokyo Institute of Technology (東京工業大学) OA exam
> 这题来自今年东京工业大学AO考试的**机械学科**

**Please answer this question in 60 minutes. **

**本题答题时间为60分钟**



![img](/maths/images/v2-47ca5ba94ba3bfcfd8ff7a9425e12267_hd.jpg)

![img](/maths/images/v2-ed1d155344c2f1c0e88042fbafc4765d_hd.jpg)

![img](/maths/images/v2-38096a4f7f35d59f7af8ee352f435110_hd.jpg)



# Answer

The answer is slow by exia.huang. If there are any problem, please tell me. Thank you.

## 問題１

$$
a_n = a_0 + \sum_{i=0}^nx_n
$$

## 問題2

$$
max\{a_n\} = a_0 + n \\
min\{a_n\} = a_0 - n
$$

## 問題3

| x1   | x2   | f(x1, x2) |
| ---- | ---- | --------- |
| 0    | 0    | 8         |
| 0    | -1   | 6         |
| 0    | 1    | 14        |
| 1    | 0    | 19        |
| 1    | -1   | 15        |
| 1    | 1    | 27        |
| -1   | 0    | 3         |
| -1   | -1   | 3         |
| -1   | 1    | 7         |

obviously, the answer is (-1, 0) or (-1, -1)



## 問題4



# Extra Analysis

## Dynamic programming

> 动态规划
>
> 动态规划的本质，是对问题状态的定义和状态转移方程的定义。

dynamic programming is a method for solving a complex problem by breaking it down into a collection of simpler subproblems.





## Fibonacci polynomial

> 斐波那契数列
>
> [斐波那契](https://en.wikipedia.org/wiki/Fibonacci) ,1175年－1250年，意大利数学家

![1539010082295](/maths/images/1539010082295.png)

```
   function fib（n）
       if n = 0 or n = 1
           return n
       return fib(n − 1) + fib（n − 2）
```

## Knapsack problem

[Knapsack problem](https://en.wikipedia.org/wiki/Knapsack_problem)

![1539010978404](/maths/images/1539010978404.png)

![Knapsack problem](/maths/images/dd9c97f255a11758a2f19098205661f90cf2fa81.svg)

## Floyd–Warshall algorithm

[Floyd–Warshall algorithm](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm)

![1539012147510](/maths/images/1539012147510.png)

![1539012157125](/maths/images/1539012157125.png)

## Dijkstra's algorithm

[Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)

Dijkstra's algorithm is an algorithm for finding the shortest paths between nodes in a graph



