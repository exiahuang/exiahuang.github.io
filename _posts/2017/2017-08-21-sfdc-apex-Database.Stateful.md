---
categories:
- Salesforce
date: 2017-08-21 08:00:34
description: Salesforce Apex Database.Stateful
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Apex Database.Stateful
update_date: 2020/05/23 23:56:51

---

# Database.Stateful を使うと、データの内容を保持した状態でバッチが走らせられた
apexでバッチを走らせる場合は、デフォルトでの200件ごとに処理を走らせる場合が多いけれれど、
その時に処理の中でカウントアップしたデータを次の処理に引き継ぎたかった。
結論から言うと、 Database.Stateful を使うと、データの内容を保持した状態でバッチが走らせられた。
具体的には以下。

```java
public with sharing class Hogehoge_Batch implements Database.Batchable<sObject>, Database.Stateful{
  
    private Integer count {get; set;}
    
  public Hogehoge_Batch(Boolean isLastBatch){
      this.count = 0;
    }
    
    public Database.QueryLocator start(Database.BatchableContext BC){
        String query = 'select id from Lead';
         return Database.getQueryLocator(query);
    }
    
    public void execute(Database.BatchableContext BC, List<Lead> scope){
        for(Lead user : scope){ 
            user.count__c = this.count;
            this.count++;
        }
        update scope;
    }
   
    public void finish(Database.BatchableContext BC){
    }
    
}
```
クラス定義の1行目の最後にくっついてる。
これがないとcountは毎回リセットされてしまう。