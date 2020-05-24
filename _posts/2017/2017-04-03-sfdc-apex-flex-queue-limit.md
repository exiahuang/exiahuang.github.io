---
categories:
- Salesforce
date: 2017-04-03 11:02:34
description: SFDC Apex Flex Queue Limit, caused by System.AsyncException, You've exceeded
  the limit of 100 jobs in the flex queue for org xxxx_org_id. Wait for some of your
  batch jobs to finish before adding more.
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Apex Flex Queue Limit
update_date: 2020/05/23 23:56:51

---

# Exception message

```java
Apex script unhandled exception by user/organization: xxxx_user_id/xxxx_org_id

Scheduled job 'xxxxxx_schedule_class' threw unhandled exception.

caused by: System.AsyncException: You've exceeded the limit of 100 jobs in the flex queue for org xxxx_org_id. Wait for some of your batch jobs to finish before adding more. To monitor and reorder jobs, use the Apex Flex Queue page in Setup.
```


# Reason of the Error

## Holding Batch Jobs in the Apex Flex Queue

With the Apex flex queue, you can submit up to 100 batch jobs.

The outcome of Database.executeBatch is as follows.
* The batch job is placed in the Apex flex queue, and its status is set to Holding.
* If the Apex flex queue has the maximum number of 100 jobs, Database.executeBatch throws a LimitException and doesn’t add the job to the queue.

# Count the flex Queue Size

```java
Integer flexQueueSize = [SELECT COUNT() FROM AsyncApexJob WHERE Status = 'Holding' FOR UPDATE];
```

# How to stop job by using apex?

```java
List<AsyncApexJob> jobs = [SELECT 
    Id,
    CreatedDate,
    CreatedById,
    JobType,
    ApexClassId,
    Status,
    JobItemsProcessed,
    TotalJobItems,
    NumberOfErrors,
    CompletedDate,
    MethodName,
    ExtendedStatus,
    ParentJobId,
    LastProcessed,
    LastProcessedOffset
 FROM AsyncApexJob
where ApexClass.name= 'bacth class name'
and Status = 'Holding'];
for(AsyncApexJob job : jobs){
    System.debug('stop job : ' + job.id + ', ApexClassId= ' + job.ApexClassId);
    System.abortJob(job.id);
}
```


# AsyncApexJob status, ジョブ状況

| status | 状況   |    説明    | 
|:------:|:-----:|:---------|
| Holding |  |  |  
| Queued | キュー | ジョブは実行待ちです。 | 
| Preparing | 準備中 | ジョブの start メソッドが呼び出されました。この状況は、レコードのバッチサイズに応じて数分かかることがあります。 | 
| Processing | 処理中 | ジョブは処理中です。 | 
| Aborted | 中止 | ジョブはユーザによって中止されました。 | 
| Completed | 完了 | ジョブはエラーあり/なしで完了しました。 | 
| Failed | 失敗 | ジョブでシステム障害が発生しました。 | 

# AsyncApexJob JobType, ジョブ種別

| status | 状況   |    説明    | 
|:------:|:-----:|:---------|
| Future | | | 
| SharingRecalculation | | | 
| ScheduledApex | | | 
| BatchApex | | | 
| BatchApexWorker | | | 
| TestRequest | | | 
| TestWorker | | | 
| ApexToken | | | 
| Queueable | | | 