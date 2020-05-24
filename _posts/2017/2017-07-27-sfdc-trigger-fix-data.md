---
categories:
- Salesforce
date: 2017-07-27 08:01:34
description: SFDC Trigger Fix Data
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Trigger Fix Data
update_date: 2020/05/23 23:56:52

---

# Trigger needs to execute before insert and before update.

Also you don't need to update the accounts at the end of the trigger you only need to do this when you want to modify records that are not being processed by then trigger.

```java
Trigger UpdateTMID on Account (before insert, before update){

 for (Account acct:Trigger.new){

  Integer i = 1;

  system.debug('This is the number of times it is has gone through the loop' +i);

  acct.PP_CLIENT_DIR_VP__c = 'JC13';

  i++;
 }
}
```