---
categories:
- Salesforce
date: 2017-10-12 08:02:34
description: Salesforce WebToLead Error
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce WebToLead Error
update_date: 2020/05/23 23:56:51

---

# Will Duplicate Matching Rules block web-to-lead submissions?

Knowledge Article Number	000212677
Description	Do Duplicate Matching Rules block Web-to-Lead submissions when the rule is set to Allow and Alert?
Resolution	Per "Duplicate Management Overview":
In some cases, if duplicate rules are set for an alert to show when potential duplicates are found, users will always be blocked from saving records and will not see a list of possible duplicates. 

This does apply to Web-to-Lead. If the duplicate matching rule is set up to block, or to allow with an alert, then Web-to-Lead submissions that match the duplicate rule will always be blocked.

To allow a duplicate Lead to be created through Web-to-Lead, you may consider:
Set criteria on your existing duplicate rule such that it does not run when the current user is the default Web-to-Lead creator.
Create another duplicate rule that runs only when the current user is the default web to lead creator, and set that rule to allow and report (without alert).


# リード変換時に重複ルールが実行されないのはなぜですか？

ナレッジ記事番号	000204497
説明	
組織が「取引開始済みのリードに入力規則が必須」権限を持っており、ユーザがリードを新規や既存の取引先責任者または取引先へ変換する場合、重複ルールで指定されたアクションに関係なく、重複ルールは保存を常にブロックします。ユーザに重複リストは表示されず、警告のメッセージが表示されます。
 
解決策	

組織が「取引開始済みのリードに入力規則が必須」権限を持っていない場合は、重複ルールは実行されません。ユーザは警告や重複リストを確認することなく、レコードを保存することができます。

リードで重複ルールを実行している組織で、関連する一致ルールは変換されたリードを比較しません。そのため、変換されたリードはリードの重複の可能性として返されることはありません。

この機能を有効化、もしくは、無効化するには、組織で次の手順を実施してください:
 
[設定] | [カスタマイズ] | [リード] | [リードの設定] にアクセスします。
[編集] をクリックして、[取引開始済みのリードに入力規則が必須] のチェックボックスをオン、もしくは、オフにします。
[保存] をクリックします。

メモ：[取引開始済みのリードに入力規則が必須] が無効化されている場合、リード変換時にトリガ、および、入力規則も無効になります。