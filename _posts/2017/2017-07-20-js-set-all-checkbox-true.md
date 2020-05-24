---
categories:
- Program
date: 2017-07-20 08:15:34
description: javascript set all checkbox true
layout: post
tags:
- javascript
title: javascript set all checkbox true
update_date: 2020/05/23 23:56:51

---

# javascript set all checkbox true
```js
var inputs = document.getElementsByTagName("input"); //or document.forms[0].elements;
for (var i = 0; i < inputs.length; i++) {
  if (inputs[i].type == "checkbox") {
    inputs[i].checked = true;
  }
}
```