---
categories:
- Salesforce
date: 2017-07-19 08:06:34
description: SFDC Apex with sharing and without sharing
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Apex with sharing and without sharing
update_date: 2020/05/23 23:56:51

---

# with sharingキーワードとwithout sharingキーワード
Apexはデフォルトでシステムモードで動作するので、全オブジェクトに対して全レコードの`編集が可能`です。

そのため、例えば、ユーザがVisualforceページでレコードを検索する場合、ユーザが参照権限を持たないレコードについても、検索できてしまいます。

ユーザが参照可能なレコードのみを検索できるようにするには、Apexクラスに`with sharing`キーワードを付与します。
これによって、ユーザに適用されているレコードレベルの`共有ルール`を強制実行することができます（ユーザモードでの動作）。

```java
public with sharing class SharingClass {

}
```

ここで注意しなくてはならないのは、with sharingキーワードを付与しても、オブジェクトのCRUD権限、項目のアクセス権限は、システムモードのままということです。ユーザがアクセスできないはずのオブジェクトや項目にアクセスできてしまいます。

`オブジェクトのCRUD権限`、`項目のアクセス権限`は、Apexでは制御できないので、開発者が、ユーザから隠されているデータを公開しないように注意して`Apexコードを書く`必要があります。

逆に、ユーザに適用されている[`共有ルール`](/Salesforce/sfdc-org-permission.html)を強制実行されないようにするには、`without sharing`キーワードを付与します。

```java
public without sharing class NoSharingClass {

}
```

with sharingキーワードもwithout sharingキーワードも付与しない場合は、呼び出し元のApexクラスの設定が有効となります。
例えば、with sharingキーワードが付与されたApexクラスから、キーワードなしのApexクラスを呼び出した場合、ユーザに適用されている`共有ルール`が強制実行されます。呼び出し位置が最上位レベルの場合（最初に呼ばれるApexクラスの場合）は、システムモードでの動作となります。

動作モードを表にまとめるとこうなります。

|呼び出し位置	    |                        キーワード                      |
|               |  なし                | without sharing | with sharing |
|最上位レベル	    | システムモード          | システムモード      | ユーザモード    |
|最上位レベル以外	| 呼び出し元のモードと同じ  | システムモード      | ユーザモード    |

ちなみに、トリガはシステムモードの動作となりますが（トリガにはキーワードを付けることができない）、トリガ内部でwith sharingキーワード付きのApexクラスを呼び出すことで、ユーザモードでの動作となります。

また、匿名ブロックは、ユーザモードでの動作となります。