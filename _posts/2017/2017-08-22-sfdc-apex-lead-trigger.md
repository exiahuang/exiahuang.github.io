---
categories:
- Salesforce
date: 2017-08-22 08:02:34
description: Salesforce Web To Lead リードの「取引の開始」時にトリガを実行する方法
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Web To Lead リードの「取引の開始」時にトリガを実行する方法
update_date: 2020/05/23 23:56:51

---

# Introduce

`リード(Lead)`オブジェクトの`「取引の開始」`を実行すると
リードの色々な項目の情報を引き継いで新たに取引先(Account)、取引先責任者(Contact)、商談(Opportunity)が作成される。

このとき、
特定のカスタム項目の値を作成されたオブジェクトのどこかに引き継ぎたい！
という要求はリードのカスタム項目の対応付けによって実現ができそうだけど、

リードにひもづけていたカスタムオブジェクトを取引先に引き継ぎたい！
といったカスタマイズをしたいと思った時、どうするのかわからなかったので その方法をメモ。

# 重要なこと

リードの取引が開始されたかどうかは`IsConverted`というフィールドを見るとわかる。
リードの取引開始によって作成された各オブジェクト（取引先、取引先責任者、商談）のIDは以下で取得する。
取引先：ConvertedAccountId
取引先責任者：ConvertedContactId
商談：ConvertedOpportunityId

# リードのトリガの実装

残念ながらリードが`IsConverted=true`になったタイミングでのトリガというのはないので
普通にbefore updateトリガなどを使う。

```java
trigger LeadTrigger on Lead (before update) {
    for (Lead lead : Trigger.new) {
        if (lead.isConverted) {
            // リードにひもづくカスタムオブジェクトを取得
            Myobj__c obj = [SELECT Id FROM Myobj__c WHERE Lead__c = :lead.id];
            
            // ConvertedAccountIdを使って取引先とひもづける
            obj.account__c = lead.convertedAccountId;
            update obj;
        }
    }
}
```