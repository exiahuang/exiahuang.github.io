---
categories:
- Salesforce
date: 2017-07-26 08:01:34
description: Can we create List controller for CampaignMember
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Can we create List controller for CampaignMember
update_date: 2020/05/23 23:56:51

---

# CampaignMember is not a supported SObjectType to use in conjunction with a StandardSetController.

Simple page to demonstrate the compilation error:
```
<apex:page standardController="CampaignMember" recordSetVar="members" />
```

Message:
```
List controllers are not supported for CampaignMember
```

# Error2
StandardSetControllerの利用について質問があります。
 
StandardSetControllerにキャンペーンメンバーを使用したquerylocatorでインスタンスを生成しようとすると、
エラーが発生してしまいます。
 
コード：
```
ApexPages.StandardSetController ssc = new ApexPages.StandardSetController(Database.getQueryLocator([SELECT Name FROM CampaignMember]));
```

エラー：
List controllers are not supported for CampaignMember
 
上記について、
・何故キャンペーンメンバーではStandardSetControllerを利用出来ないのか？
・キャンペーンメンバーを用いたStandardSetControllerを生成する方法はないのか？
ご存知の方はご教授の程よろしくお願いします。