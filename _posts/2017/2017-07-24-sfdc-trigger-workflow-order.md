---
categories:
- Salesforce
date: 2017-07-24 08:01:34
description: 自動化ルール、および、Apex トリガーはどのような順番で処理されますか？
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: 自動化ルール、および、Apex トリガーはどのような順番で処理されますか？
update_date: 2020/05/23 23:56:52

---

# 自動化ルール、および、Apex トリガーはどのような順番で処理されますか？
下記が、レコードに適用される salesforce ロジックの順序です。
- 古いレコードをデータベースからロード（または、新しい挿入の初期化）
- 新しいレコードの値で古い値を上書き
- システムの入力規則（商談商品を挿入する場合、システムの入力規則に加えてカスタム入力規則が実行されます）
- すべての before トリガを実行（EE / UE のみ）
- カスタム入力規則
- レコードをデータベースに保存（しかし、コミットされていない）
- レコードをデータベースから再ロード
- すべての after トリガを実行（EE / UE のみ）
- 割り当てルール
- 自動応答ルール
- ワークフロー ルール
- プロセス
- エスカレーション ルール
- 積み上げ集計数式の値の更新（存在する場合）
- データベースのコミット
- コミット後のロジック（メールの送信）

# 追加のメモ:
上記の各グループ内の実行順序を制御する方法はありません。
承認プロセスや時間依存のアクションに基づいて実行されるワークフロー項目の更新は、いかなるルールもトリガーしません。
数式項目はこの方法では実行されません。それらは、項目に任意の方法でアクセスするたびにその結果を計算しリアルタイムに表示します。そのため、例えば、ワークフロー ルールがその条件や式に数式項目を使用している場合、ワークフロー ルールの条件がチェックされたときに、その数式項目は評価されます。

実行順序の詳細な追加情報について、次の記事を参照してください（英語）。
[apex_triggers_order_of_execution](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers_order_of_execution.htm)