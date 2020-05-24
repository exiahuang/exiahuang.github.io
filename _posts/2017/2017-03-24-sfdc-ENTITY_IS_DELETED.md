---
categories:
- Salesforce
date: 2017.03.24 17:08:00
description: Salesforce apex updateあるいはdeleteしたらDmlExceptionが出た
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce apex updateあるいはdeleteしたらDmlExceptionが出た
update_date: 2020/05/23 23:56:51

---

# Salesforce apex updateあるいはdeleteしたらDmlExceptionが出た

```
First error: Update failed.
First exception on row 0 with id a08xxxxxxxxxxxxxxx; 
first error: ENTITY_IS_DELETED, entity is deleted: []
```

削除したオブジェクトは参照でできないから。


# 「ENTITY_IS_DELETED」なのどコードの意味は？

<a target="_blank" class="btn" href="https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_concepts_core_data_objects.htm">SFDC Developer Guide</a>

<div class="note primary">You can’t reference an object that has been deleted. 
This status code occurs only in API version 10.0 and later. 
Previous releases of the API use INVALID_ID_FIELD for this error.
</div>