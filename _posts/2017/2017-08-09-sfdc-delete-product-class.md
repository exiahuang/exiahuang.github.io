---
categories:
- Salesforce
date: 2017-08-09 08:00:34
description: Salesforce Delete Product Class・Trigger・etc
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Delete Product Class・Trigger・etc
update_date: 2020/05/23 23:56:51

---

# 本番組織から Apex クラス、または、トリガを無効または削除する方法

削除または無効にする手順
 
1. Force.com IDE はインストールされている必要があります。
2. IDE を使用しているサンドボックスインスタンスへ接続し、削除したいクラス、または、トリガを見つけます。
3. 一致している .xml ファイルを開き、XML タグのステータスを "Active" から "Deleted" へ変更します。
4. あるいは、トリガを無効にするために、 "Inactive" へ変更します。
注意: Apex クラスのステータスは "Active" または "Deleted" へのみ変更することができ、 "Inactive" へ変更することはできません。
5. ファイルを保存します。
6. Ctrl-クリックを使用し、二つのファイル（Code および XML）を選択します。そして、それらのうちのひとつで右クリックします。 
7. Force.com | Deploy to Server を選択します。
8. 本番組織の証明書を提供し、その手順に従います。

# more help
[more help](https://help.salesforce.com/articleView?id=000006188&language=ja&type=1)