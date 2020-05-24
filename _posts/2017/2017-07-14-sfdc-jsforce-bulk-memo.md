---
categories:
- Salesforce
date: 2017-07-14 08:05:34
description: SFDC JSForce Memo
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC JSForce Memo
update_date: 2020/05/23 23:56:51

---

# Encoding error ?
```js
// Provide records
var accounts = [
  { Name : 'Account #1' },
  { Name : 'テスト #2' },
  { Name : 'Account #3' },
];
// Create job and batch
var job = conn2.bulk.createJob("Account", "insert");
var batch = job.createBatch();
// start job
batch.execute(accounts);
// listen for events
batch.on("error", function(batchInfo) { // fired when batch request is queued in server.
  console.log('Error, batchInfo:', batchInfo);
});
batch.on("queue", function(batchInfo) { // fired when batch request is queued in server.
  console.log('queue, batchInfo:', batchInfo);
  batch.poll(1000 /* interval(ms) */, 20000 /* timeout(ms) */); // start polling - Do not poll until the batch has started
});
batch.on("response", function(rets) { // fired when batch finished and result retrieved
  for (var i=0; i < rets.length; i++) {
    if (rets[i].success) {
      console.log("#" + (i+1) + " loaded successfully, id = " + rets[i].id);
    } else {
      console.log("#" + (i+1) + " error occurred, message = " + rets[i].errors.join(', '));
    }
  }
  // ...
});
```

# bug error memo 2
```
var query = conn.query("SELECT Name, Type, BillingState, BillingCity, BillingStreet FROM Account limit 3");
var job = conn2.bulk.createJob("Account", "insert");
var batch = job.createBatch();
query.pipe(batch);
batch.on('queue', function() {
  jobId = job.id;
  batchId = batch.id;
  console.log(job.id);
  console.log(batch.id);
  //...
});
```

# memo 3
```
var query = conn.query("SELECT Name, Type, BillingState, BillingCity, BillingStreet FROM Account limit 3", function(err, result) {
  if (err) { return console.error(err); }
  console.log("total : " + result.totalSize);
  console.log("fetched : " + result.records.length);


  var job = conn2.bulk.createJob("Account", "insert");
  var batch = job.createBatch();
    batch.execute(result.records);
    // listen for events
  batch.on("error", function(batchInfo) { // fired when batch request is queued in server.
    console.log('Error, batchInfo:', batchInfo);
  });
  batch.on("queue", function(batchInfo) { // fired when batch request is queued in server.
    console.log('queue, batchInfo:', batchInfo);
    batch.poll(1000 /* interval(ms) */, 20000 /* timeout(ms) */); // start polling - Do not poll until the batch has started
  });
  batch.on("response", function(rets) { // fired when batch finished and result retrieved
    for (var i=0; i < rets.length; i++) {
      if (rets[i].success) {
        console.log("#" + (i+1) + " loaded successfully, id = " + rets[i].id);
      } else {
        console.log("#" + (i+1) + " error occurred, message = " + rets[i].errors.join(', '));
      }
    }
    // ...
  });

});
```

# RecordStream
```
var query = conn.query("SELECT Name, Type, BillingState, BillingCity, BillingStreet FROM Account limit 3");
query.pipe(jsforce.RecordStream.map(function(r) {
     console.log(r);
   }));
```



# Read Meta Data
```js
var fullNames = [ 'Account', 'Contact' ];
conn.metadata.read('CustomObject', fullNames, function(err, metadata) {
  if (err) { console.error(err); }
  for (var i=0; i < metadata.length; i++) {
    var meta = metadata[i];
    console.log("Full Name: " + meta.fullName);
    console.log("Fields count: " + meta.fields.length);
    console.log("Sharing Model: " + meta.sharingModel);
  }
});
```