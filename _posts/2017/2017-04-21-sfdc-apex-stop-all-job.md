---
categories:
- Salesforce
date: 2017-04-21 22:02:34
description: SFDC Apex Stop All Job.
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Apex Stop All Job
update_date: 2020/05/23 23:56:51

---

# Exception message

```java
for (AsyncApexJob job :[SELECT Id FROM AsyncApexJob where  Status in ('Holding', 'Processing')] ) {
    System.abortJob(job.Id);
}
```