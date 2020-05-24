---
categories:
- Salesforce
date: 2017-07-20 08:09:34
description: SFDC Trigger
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Trigger Review
update_date: 2020/05/23 23:56:52

---

# Apexトリガのレビューポイントは、次の3つです。
- 複数レコード更新を考慮した実装となっているか？
- ガバナ制限を理解した実装となっているか？
- Apexトリガの実行順序を正しく考慮した実装となっているか？

# 複数レコード更新を考慮
Apexトリガコンテキスト内ではTrigger.NewやTrigger.Old変数にレコードのリストが格納されています。このリストには`最大200件`のリストが格納されている可能性があります。

# ガバナ制限
1コンテキスト内で発行可能なSOQLやDMLには上限があります。
for文内で、SOQLやDMLを発行していないか確認します。

# 実行順序
ここで特に問題となりやすいのは、ワークフロールールなどで項目自動更新が実装されている場合、画面などからの通常の更新の後に、`再度項目自動更新`によるApexトリガが発火することです。
トリガの発火状態を保持するstaticな変数を利用して、2重起動を抑止させましょう。

# ワークフローとトリガを同時に使用する際トリガを２回起動しない方法はありますか
専用の Static field を持つクラスを使用し、トリガーを初回起動かどうかを判定することで、上記現象を回避することが可能です。

※　
Salesforceの Static field はリクエストスコープの中だけで共有され、サーバー全体、または全体組織で共有されません。
このことから Static field の値を利用して、トリガーの初回の発動が否かを判断することが可能です。

※
下記、リファレンスに、2度目に実行されたトリガを意図的にエラーにするサンプルが紹介されています。
こちらを参考にしていただければ幸いです。

Using Static Methods and Variables
https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_static.htm

日本語版(静的メソッドと変数の使用)
https://developer.salesforce.com/docs/atlas.ja-jp.apexcode.meta/apexcode/apex_classes_static.htm
※
サンプルコード
```
public class p {
public static boolean firstRun = true;
}
```

```
trigger Trigger_001 on Test__c (before update) {
if(p.firstRun==true){
system.debug('1回目の起動です。');
p.firstRun=false;
}
else{
system.debug('2回目の起動です。');
}
}
```