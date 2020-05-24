---
categories:
- Salesforce
date: 2017-07-25 08:01:34
description: SFDC Release Memo
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Release Memo
update_date: 2020/05/23 23:56:52

---

# 変更セット（クラウドデプロイ）の実行が失敗してしまう
各エラーの意味は以下の通りになります。

# カスタムオブジェクトの定義
## Can't set recordTypeTrackHistory on an object with no record types

変更セット内にオブジェクトの定義情報のみが含められており
レコードタイプ自体が変更セットに追加されていないことを示しております。
オブジェクトのメタデータとしては、レコードタイプが存在するという情報が
含まれているにも関わらず、実際の変更セット内にレコードタイプ自体が
存在しないため本エラーが発生しております。


## Cannot set ControlledByParent on a CustomObject without a MasterDetail relationship field

変更セット内にオブジェクトの定義情報のみが含められており
主従関係項目が変更セットに追加されていないことを示しております。
オブジェクトのメタデータとしては、主従関係の項目が存在するという情報が
含まれているにも関わらず、実際の変更セット内に主従関係項目自体が
存在しないため本エラーが発生しております。

変更セットにレコードタイプや主従関係項目を追加して、再度アップロードしてください。

## ​Cannot set sharingModel to ControlledByParent on a CustomObject without a MasterDetail relationship field
上記のエラーは、主従関係を持つオブジェクトをリリースする際に、受信変更セット内に該当する主従関係の項目が含まれていない場合に発生します。
カスタムオブジェクトのメタデータとしては、主従関係の項目が存在するという情報が含まれているにも関わらず、
主従関係の項目が存在しないため、エラーを表示します。
このエラーは、変更セット内に主従関係の項目を含めることで解消します。

# Release order
## Step1. Object作成,　ラベル作成, 
object
labels(手動修正確認ラ)

## Step2. workflow, プロセスビルダー
workflow
flow

## Step3. Class,Trigger,page,layout,report
Class
TestClass
Trigger
page
layout

## Step4. Report,ReportType
reports
ReportType


## Step5.　手動作成
タブ
profiles設定