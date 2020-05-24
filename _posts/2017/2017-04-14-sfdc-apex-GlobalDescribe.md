---
categories:
- Salesforce
date: 2017-04-14 22:05:34
description: SFDC Apex GlobalDescribe
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Apex GlobalDescribe
update_date: 2020/05/23 23:56:51

---

# SFDC Apex GlobalDescribe Example

```java
public static void DescribeSObjectExample(){
        Map<String, Schema.SObjectType> smap = Schema.getGlobalDescribe();
        Schema.SObjectType sobj = smap.get('InputData__c');
        Schema.DescribeSObjectResult sr = sobj.getDescribe();
        // field
        Map<String, Schema.SObjectField> fmap = sr.fields.getMap();

        List<MyObject__c> inputListOrg = [SELECT id,API__c FROM MyObject__c];
        Map<String, MyObject__c> inputMapOrg = new Map<String, MyObject__c>();
        for(MyObject__c tmp: inputListOrg){
          inputMapOrg.put(tmp.API__c, tmp);
        }

        List<MyObject__c> inputList = new List<MyObject__c>();
        for (String fieldKey : fmap.keySet()) {
            Schema.SObjectField f = fmap.get(fieldKey);
            Schema.DescribeFieldResult fr = f.getDescribe();

            if(!fr.isCustom() ) continue;
            System.debug('***** field is Custom: ' + fr.isCustom());
            System.debug('***** field label: ' + fr.getLabel());
            System.debug('***** field API reference name: ' + fr.getName());
            System.debug('***** field type: ' + fr.getType());
            System.debug('------>fr ' + fr);

            MyObject__c obj = new MyObject__c();
            obj.Name = fr.getLabel();
            obj.API__c = fr.getName();
            
            if(inputMapOrg.containsKey(obj.API__c)) continue;

            inputList.add(obj);
        }
        insert inputList;
}
```