---
categories:
- Program
date: 2017-08-03 08:01:34
description: VBA Replace NG char
layout: post
tags:
- Program
- VBA
title: VBA Replace NG char
update_date: 2020/05/23 23:56:53

---

# ファイル名に使えない文字を取り除くコード

下記のプログラムで、対象の文字を取り除くことができます。非常に原始的な方法ですが。。。
全部取り除くと空文字列になってしまうかもしれない場合は二番目の引数（オプショナル）に置換用の文字を指定することができます。

```vba
Public Function replaceNGchar(ByVal sourceStr As String, _
        Optional ByVal replaceChar As String = "") As String

    Dim tempStr As String
    
    tempStr = sourceStr
    tempStr = Replace(tempStr, "\", replaceChar)
    tempStr = Replace(tempStr, "/", replaceChar)
    tempStr = Replace(tempStr, ":", replaceChar)
    tempStr = Replace(tempStr, "*", replaceChar)
    tempStr = Replace(tempStr, "?", replaceChar)
    tempStr = Replace(tempStr, """", replaceChar)
    tempStr = Replace(tempStr, "<", replaceChar)
    tempStr = Replace(tempStr, ">", replaceChar)
    tempStr = Replace(tempStr, "|", replaceChar)
    tempStr = Replace(tempStr, "[", replaceChar)
    tempStr = Replace(tempStr, "]", replaceChar)

    replaceNGchar = tempStr
End Function
```