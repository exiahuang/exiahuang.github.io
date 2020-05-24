---
categories:
- Salesforce
date: 2017-07-28 08:04:34
description: SFDC DataBackup
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC DataBackup
update_date: 2020/05/23 23:56:51

---

# Bulk API の制限 Bulk API Limits
[Read More](https://developer.salesforce.com/docs/atlas.en-us.208.0.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_bulkapi.htm)

## Batch size バッチサイズ
- Batches for data loads can consist of a single CSV, XML, or JSON file that is no larger than 10 MB.
- A batch can contain a maximum of 10,000 records.
- A batch can contain a maximum of 10,000,000 characters for all the data in a batch.
- A field can contain a maximum of 32,000 characters.
- A record can contain a maximum of 5,000 fields.
- A record can contain a maximum of 400,000 characters for all its fields.
- A batch must contain some content or an error occurs.

- データ読み込みのバッチは 10 MB 以下の単一の CSV ファイル、XML ファイル、または JSON ファイルで構成できます。
- 1 つのバッチには、最大で 10,000 件のレコードを含めることができます。
- 1 つのバッチには、最大で 10,000,000 文字のデータを含めることができます。
- 1 つの項目には、最大で 32,000 文字を含めることができます。
- 1 つのレコードには、最大で 5,000 項目を含めることができます。
- 1 つのレコードに含まれる項目には、合計で最大 400,000 文字を含めることができます。
- バッチには何らかのコンテンツが必要です。バッチが空の場合はエラーが返されます。

## Binary content バイナリ型のコンテンツ
- The length of any file name can’t exceed 512 bytes.
- A zip file can’t exceed 10 MB.
- The total size of the unzipped content can’t exceed 20 MB.
- A maximum of 1,000 files can be contained in a zip file. Directories don’t count toward this total.

- ファイル名の最大長は 512 バイトです。
- zip ファイルの最大サイズは 10 MB です。
- コンテンツの最大合計サイズは、圧縮解除した状態で 20 MB です。
- 1 つの zip ファイルに含めることができるファイル数は最大で 1,000 ファイルです。ディレクトリはファイル数にはカウントされません。

# Using Data Loader from the command line
[Using Data Loader from the command line](https://developer.salesforce.com/page/Using_Data_Loader_from_the_command_line#File_interactions_and_best_practices)

# What is differnt between Export and Export all in DataLoader?
Export :  It is used to export the Salesforce Data(excluding recycle bin's data) into your local  system.
Export All :  It is used to export the Salesforce Data(including recycle bin's data) into your local system.

# Use Bulk API
データローダで大量データを登録する場合は、Bulk APIを使用します。Bulk APIは設定画面の「Use Bulk API」にチェックをつけると使用できます。チェックをつけるとBach Sizeが2000件に自動で変更されます。これで通常のINSERT処理よりも効率よく登録処理が実行されます。

『1MB = 1000KB』でレコード1件あたり『約2KB』となります。『250000 / 2 = 125000』となるので余裕をみて123000件の登録処理を行ってみることにしました。

実際に大量データの処理を行う場合は対象項目が多くなったり、トリガーやワークフローが入っていたりして、もう少し時間がかかるかと思いますが、シンプルな登録処理なら12万件ぐらいあってもこんな感じで簡単に登録できました。


# other 
sfdc-exportjs