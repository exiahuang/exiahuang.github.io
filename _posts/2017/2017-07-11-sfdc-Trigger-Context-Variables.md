---
categories:
- Salesforce
date: 2017-07-11 08:01:34
description: Salesforce Trigger Context Variables
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Trigger Context Variables
update_date: 2020/05/23 23:56:52

---

# Trigger Context Variables
All triggers define implicit variables that allow developers to access run-time context. These variables are contained in the System.Trigger class.

Apex Trigger コンテキスト変数についてです。Trigger.newやTrigger.oldは良く使用しますが他にも便利な変数が用意されています。

## Trigger.isExecuting

現在のコンテキストがApexトリガーから呼び出されている場合に、Trueを返します。

## Trigger.isInsert

レコードの新規作成処理によるApexトリガーの場合に、Trueを返します。

## Trigger.isUpdate

レコードの更新処理によるApexトリガーの場合に、Trueを返します。

## Trigger.isDelete

レコードの削除処理によるApexトリガーの場合に、Trueを返します。

## Trigger.isUndelete

レコードの復元処理によるApexトリガーの場合に、Trueを返します。

## Trigger.isBefor

Before Triggerの場合に、Trueを返します。

## Trigger.isAfter

After Triggerの場合に、Trueを返します。

## Trigger.new

sObjectレコードの新しいバージョンのリストを返します。

## Trigger.old

sObjectレコードの古いバージョンのリストを返します。

## Trigger.newMap

sObjectレコードの新しいバージョンのマップを返します。
キーはID項目になります。

## Trigger.oldMap

sObjectレコードの古いバージョンのマップを返します。
キーはID項目になります。

## Trigger.size

新旧両方のトリガーの呼び出し内のレコードの合計数を返します。

# doc
[Trigger Context Variables](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers_context_variables.htm)