---
categories:
- Salesforce
date: 2017-08-04 08:00:34
description: Salesforce Apex auto create soql
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Apex auto create soql
update_date: 2020/05/23 23:56:51

---

# Salesforce Apex auto create soql

```java
Map<String, Schema.SObjectType> smap = Schema.getGlobalDescribe();

for(Schema.SObjectType sobj : smap.Values()){
    Schema.DescribeSObjectResult sr = sobj.getDescribe();
    // field
    Map<String, Schema.SObjectField> fmap = sr.fields.getMap();

    List<string> fields = new List<string>();
    for (String fieldKey : fmap.keySet()) {
        Schema.SObjectField f = fmap.get(fieldKey);
        Schema.DescribeFieldResult fr = f.getDescribe();
        fields.add(fr.getName());

        // if(!fr.isCustom() ) continue;
        // System.debug('***** field is Custom: ' + fr.isCustom());
        // System.debug('***** field label: ' + fr.getLabel());
        // System.debug('***** field API reference name: ' + fr.getName());
        // System.debug('***** field type: ' + fr.getType());
        // System.debug('------>fr ' + fr);
    }

    String soql = 'SELECT ';
    soql += string.join(fields,' , ');
    soql += ' FROM ' + sr.getName();
    System.debug(soql);

}
```