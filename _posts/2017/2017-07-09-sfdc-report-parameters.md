---
categories:
- Salesforce
date: 2017-07-09 08:00:34
description: Salesforce Report Parameters
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Report Parameters
update_date: 2020/05/23 23:56:52

---

# Salesforce レポート URL Parameters

URLパラメータ	意味	値
break[n]（nは番号）	集計項目	項目名を指定 例）break0=OWNER
colDt_c	期間条件-日付項目	項目名を指定 例）colDt_c=DUE_DATE
colDt_q	期間条件-範囲	curfy：当会計年度、current：当会計四半期、cury：本年、currentq：当四半期、thismonth：今月、thisweek：今週、today：今日、last7：過去7日間。custom：カスタム など
sdate	期間条件-開始	yyyy/MM/dd
edate	期間条件-終了	yyyy/MM/dd
scope	表示スコープ	user：私の○○○、team：私のチームの○○○、organization：すべての○○○
pc[n]（nは番号）	条件-項目	項目名を指定 例）pc0=LAST_ACTIVITY
pn[n]（nは番号）	条件-条件	eq：次の文字列と一致する、ne：次の文字列と一致しない、lt：＜、gt：＞、le：＜＝、ge：＞＝、co：次の文字列を含む、nc：次の文字列を含まない、sw：次の文字列で始まる、in：次の値を含む、ex：次の値を含まない
pv[n]（nは番号）	条件-値	
details	詳細表示	yes：表示、no：非表示
sort	ソート項目	項目名を指定 例）sort=ACCOUNT.NAME