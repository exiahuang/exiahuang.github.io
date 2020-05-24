---
categories:
- Salesforce
date: 2017-09-11 08:02:34
description: Salesforce DMLOptions.DuplicateRuleHeader クラス
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce DMLOptions.DuplicateRuleHeader クラス
update_date: 2020/05/23 23:56:51

---

# 次の例は、重複と識別された取引先レコードを保存する方法を示します。重複エラーを反復処理する方法についての詳細は、「DuplicateError クラス」を参照してください。
```java
Database.DMLOptions dml = new Database.DMLOptions(); 
dml.DuplicateRuleHeader.allowSave = true;
dml.DuplicateRuleHeader.runAsCurrentUser = true;
Account duplicateAccount = new Account(Name='dupe');
Database.SaveResult sr = Database.insert(duplicateAccount, dml);
if (sr.isSuccess()) {
	System.debug('Duplicate account has been inserted in Salesforce!');
}
```


# Example2
```java
// Create two accounts, one of which is missing a required field
Account[] accts = new List<Account>{
    new Account(Name='Account1'),
    new Account()};
Database.SaveResult[] srList = Database.insert(accts, false);

// Iterate through each returned result
for (Database.SaveResult sr : srList) {
    if (sr.isSuccess()) {
        // Operation was successful, so get the ID of the record that was processed
        System.debug('Successfully inserted account. Account ID: ' + sr.getId());
    }
    else {
        // Operation failed, so get all errors                
        for(Database.Error err : sr.getErrors()) {
            System.debug('The following error has occurred.');                    
            System.debug(err.getStatusCode() + ': ' + err.getMessage());
            System.debug('Account fields that affected this error: ' + err.getFields());
        }
    }
}
```