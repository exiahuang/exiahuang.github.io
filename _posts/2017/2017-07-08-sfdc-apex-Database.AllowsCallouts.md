---
categories:
- Salesforce
date: 2017-07-08 08:01:34
description: Salesforce Apex Database.AllowsCallouts
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Apex Database.AllowsCallouts
update_date: 2020/05/23 23:56:51

---

# Apex Batch（Database.AllowsCallouts）+ Apex SOAP or Apex HTTP

Salesforceには、Salesforceからバッチで大量データを外部システムに対して送信するAPIは提供されていません。そのため、大量データを処理するという観点からApex Batchを使用します。
具体的には、Database.Batchableインターフェースを実装したApex Batchのクラスに、さらにDatabase.AllowCalloutsインターフェースを実装することで、Apex Batchからコールアウトすることが可能になります。
この処理方式は非同期で外部システムと連携を行うため、連携の成功／失敗を適切に確認できる手段や、連携に失敗した場合のリカバリ方法などは十分に検討した方がよいでしょう。
また、大量データを処理することが想定されるため、ガバナ制限の抵触には注意が必要になります。

`Database.AllowCallouts`インターフェースをimplementsする
これを実装しないと、以下のように`System.LimitException`が発生します。

`System.LimitException: Too many callouts: 1`