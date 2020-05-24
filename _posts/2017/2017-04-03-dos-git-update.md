---
categories:
- Program
date: 2017-04-03 22:18:39
description: windows批处理脚本 , Windows Batch Script For Git.
layout: post
tags:
- windows
- IT
title: Windows Batch Script For Git
update_date: 2020/05/23 23:56:51

---

# Windows Batch Script For Git

``` bash
@echo off
rem given path
set path1=%cd%
set path2=%cd%\Salesforce
rem eg:
rem set path3=C:\
rem set path4=D:\
setlocal enabledelayedexpansion
set /a total_count=0
set /a path_index=1
if "%1"=="" (
  echo =================== start
  rem traversal each path
  for /L %%i in (1,1,1000) do (
    if defined path%%i if exist !path%%i! (
      echo ^>^>^>^>^>^>^>^>^>^>^>^>^>^>^>^>^>^>^> scaning !path%%i!
      for /D %%r in (!path%%i!\*) do (
        if exist %%r\.git (
          echo ------------------- %%r
          git --git-dir "%%r\.git" --work-tree "%%r" pull
          set /a total_count=total_count+1
        )
        if exist %%r\.gitmodules (
          echo ------------------- %%r submodules
          cd /d %%r && git submodule foreach git pull origin master
        )
        )
      echo ^<^<^<^<^<^<^<^<^<^<^<^<^<^<^<^<^<^<^< !path%%i! done
    ) else (
      goto end
    )
  )
  echo =================== !total_count! pulled
) else (
  if exist %1\.git (
    echo ------------------- %1
    git --git-dir "%1\.git" pull
  )
  if exist %1\.gitmodules (
    echo ------------------- %1 submodules
    cd /d %1 && git submodule foreach git pull origin master
  )
)
:end
pause
```