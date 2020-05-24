---
categories:
- Salesforce
date: 2017-07-25 08:02:34
description: SFDC Event WhoId WhatId
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Event WhoId WhatId
update_date: 2020/05/23 23:56:51

---

# SalesforceのEvent、TaskオブジェクトのAccountIdの挙動についてまとめます。
AccountIdに値が入る条件は以下になります。
|No	|名前(WhoId)	   |関連先(WhatId)   |AccountId|
|1	|リード	       |-	             |-        |
|2	|取引先責任者   |-				 |取引先責任者の取引先ID|
|3	|-	           |取引先			 |取引先ID |
|4	|取引先責任者   |取引先			 |取引先ID |
|5	|取引先責任者   |商談	         |取引先責任者の取引先ID |
|6	|-				|商談			 |- |

AccountIdに値が入る条件は、上記の表No.2～5になります。
例外として
No.2のように名前(WhoId)が取引先責任者の場合は、AccountIdに取引先責任者の取引先IDが入るが、
No.4のように名前(WhoId)が取引先責任者でかつ、関連先に「取引先」が設定されている場合のみ
AccountIdは関連先の取引先IDによって上書きされます。

# Event Insert Example
```java
Event obj = new Event();
obj.WhoId = ContactId; //取引先責任者Id
obj.WhatId = OpportunityId; //商談Id
obj.Subject = 'サブジェクト'; // Subject
obj.StartDateTime = Datatime.now(); //  開始
obj.EndDateTime = Datatime.now();  //  終了
obj.Description = 'Description';
```