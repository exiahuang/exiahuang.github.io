---
categories:
- Salesforce
date: 2017-07-08 08:00:34
description: Salesforce Field Sets,項目セット
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Field Sets,項目セット
update_date: 2020/05/23 23:56:51

---

# Field Sets　項目セット
 
Force.comで言うと、今回の「項目セット」や「カスタム設定」「カスタム表示ラベル」「静的リソース」あたりを使っている組織は
メンテナンスがしやすい傾向があります。

## outputFieldとinputFieldの場合

StandardControllerでoutputFieldとinputFieldを使った単純なパターンです。
```jsp
<apex:page standardController="Opportunity">
  <apex:form >
    <apex:pageBlock mode="edit" title="商談 項目セットサンプル画面">

      <apex:pageMessages />
      <apex:pageBlockButtons >
        <apex:commandButton value="保存" action="{!save}"/>
        <apex:commandButton value="キャンセル" action="{!cancel}" />
      </apex:pageBlockButtons>

      <apex:pageBlockSection columns="2" title="outputFieldのサンプル">
        <apex:repeat value="{!$ObjectType.Opportunity.FieldSets.Set01}" var="s"> 
          <apex:outputField value="{!Opportunity[s]}"/>
        </apex:repeat>
      </apex:pageBlockSection>

      <apex:pageBlockSection columns="2" title="inputFieldのサンプル">
        <apex:repeat value="{!$ObjectType.Opportunity.FieldSets.Set01}" var="s"> 
          <apex:inputField value="{!Opportunity[s]}" required="{!s.Required}"/>
        </apex:repeat>
      </apex:pageBlockSection>

    </apex:pageBlock>
  </apex:form>
</apex:page>
```

項目セットには$ObjectType.[オブジェクト名].FieldSets.[項目セット名]でアクセスしています。
また、inputfiledにはrequiredを指定して、先ほど作った項目セット側で必須定義したものを必須入力にしています。
項目側が必須になっているようなフェーズ項目等は、項目セット側で必須じゃなく設定することもできますが、
当然ながら保存時にエラーになります。
inputField側でrequiredを指定しなければ、項目側の必須設定によって、赤マークが出たりするようです。

Visualforceページ名に?id=[商談SFID] を付けて見るとこんな感じ

## outputTextとinputTextの場合

outputTextとinputTextを使う場合はラベル名を引っ張ってこないといけないので、$ObjectType.Opportunity.Fields[s].labelとかで取ります。

```jsp
<apex:page standardController="Opportunity">
  <apex:form >
    <apex:pageBlock mode="edit" title="商談 項目セットサンプル画面">

      <apex:pageMessages />
      <apex:pageBlockButtons >
        <apex:commandButton value="保存" action="{!save}"/>
        <apex:commandButton value="キャンセル" action="{!cancel}" />
      </apex:pageBlockButtons>

      <apex:pageBlockSection columns="2" title="outputTextのサンプル">
        <apex:repeat value="{!$ObjectType.Opportunity.FieldSets.Set01}" var="s"> 
          <apex:outputText value="{!Opportunity[s]}" label="{!$ObjectType.Opportunity.Fields[s].label}" />
        </apex:repeat>
      </apex:pageBlockSection>

      <apex:pageBlockSection columns="2" title="inputTextのサンプル">
        <apex:repeat value="{!$ObjectType.Opportunity.FieldSets.Set01}" var="s"> 
          <apex:inputText value="{!Opportunity[s]}" label="{!$ObjectType.Opportunity.Fields[s].label}" required="{!s.Required}"/>
        </apex:repeat>
      </apex:pageBlockSection>

    </apex:pageBlock>
  </apex:form>
</apex:page>
```

## Apexで使う場合

Schema.FieldSetとSchema.FieldSetMemberメソッドを使って取得することが可能。
使うとこだけ見ると以下のような感じ。
```java
public List<Schema.FieldSetMember> getFields() {
	return SObjectType.Opportunity.FieldSets.Set01.getFields();
}

private Opportunity getOpportunity() {
	String query = 'SELECT ';
	for(Schema.FieldSetMember f : this.getFields()) {
		query += f.getFieldPath() + ', ';
	}
	query += 'Id, Name FROM Opportunity LIMIT 1';
	return Database.query(query);
}
```

## sfdc doc
[sfdc doc](https://developer.salesforce.com/docs/atlas.ja-jp.pages.meta/pages/pages_dynamic_vf_field_sets.htm)
- 1 ページで最大 50 個の項目セットを参照できます。
- 項目セットには必須ではない項目のみを追加することをお勧めします