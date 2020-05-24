---
categories:
- Salesforce
date: 2017-08-31 08:02:34
description: Salesforce Report Parameter
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Report Parameter
update_date: 2020/05/23 23:56:52

---

# 
サンプルで言うと
https://<インスタンス名>.salesforce.com/<レポートID>?pc0=OPPORTUNITY_NAME&pn0=co&pv0=Salesforce
の部分です。
 
もっと言うと上記のようなフルパスではなく、相対パスで書けばインスタンス名を気にする必要がなくなるので、そちらをお勧めします。
相対パスは下記のようにsalesforce.com以降から書きます。
/<レポートID>?pc0=OPPORTUNITY_NAME&pn0=co&pv0=Salesforce

＜レポートの項目名＞はAPI参照名ではなく、もっと内部的なIDのことですね。
サンプルでは標準項目の「商談名」なので分かりやすく「OPPORTUNITY_NAME」となっていますが、