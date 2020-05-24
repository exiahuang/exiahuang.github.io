---
categories:
- Salesforce
date: 2017-07-08 08:10:34
description: 未対応の Apex 例外のメール通知受信者の設定
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce 未対応の Apex 例外のメール通知受信者の設定
update_date: 2020/05/23 23:56:51

---

# 未対応の Apex 例外のメール通知受信者の設定

Apex コードで未対応の例外が発生したときにメールを受信するメールアドレスを設定します。以前は、これらのメールは失敗したクラスまたはトリガを最後に変更した開発者のみに送信されていました。Salesforce 組織のユーザと任意のメールアドレスにも通知できるようになりました。

未対応の例外メールは、失敗したクラスまたはトリガの LastModifiedBy 項目で指定された開発者にデフォルトで送信されます。さらに、Salesforce 組織のユーザと任意のメールアドレスにメールを送信することもできます。これらのメール通知を設定するには、[設定] から [クイック検索] ボックスに「Apex 例外メール」と入力し、[Apex 例外メール] を選択します。Tooling API オブジェクトの ApexEmailNotification を使用して、Apex 例外メールを設定することもできます。