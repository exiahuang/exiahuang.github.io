---
categories:
- Salesforce
date: 2017-04-13 22:12:34
description: sfdc two way to get apex testcode list
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: sfdc two way to get apex testcode list
update_date: 2020/05/23 23:56:51

---

# use `ApexTestQueueServlet` to get testcode list

Call the `_ui/common/apex/test/ApexTestQueueServlet?action=GET_TESTS`,
It will return json string.

# use apexclass

```js
```