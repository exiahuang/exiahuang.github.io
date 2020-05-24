---
categories:
- Salesforce
date: 2017-07-21 08:05:34
description: SFDC String Equal
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC String Equal
update_date: 2020/05/23 23:56:52

---

# String Equal and ==
```js
String s1 = 'abc';
String s2 = 'ABC';

System.debug('==での比較① : ' + (s1==s2));
System.debug('equalsでの比較① : ' + s1.equals(s2));
```

# Result
```
37.0 APEX_CODE,DEBUG;APEX_PROFILING,INFO;CALLOUT,INFO;DB,INFO;SYSTEM,DEBUG;VALIDATION,INFO;WORKFLOW,INFO
Execute Anonymous: String s1 = 'abc';
Execute Anonymous: String s2 = 'ABC';
Execute Anonymous: 
Execute Anonymous: System.debug('==での比較① : ' + (s1==s2));
Execute Anonymous: System.debug('equalsでの比較① : ' + s1.equals(s2));
13:30:31.6 (6879801)|EXECUTION_STARTED
13:30:31.6 (6883812)|CODE_UNIT_STARTED|[EXTERNAL]|execute_anonymous_apex
13:30:31.6 (7352260)|USER_DEBUG|[4]|DEBUG|==での比較① : true
13:30:31.6 (7393808)|USER_DEBUG|[5]|DEBUG|equalsでの比較① : false
13:30:31.7 (7420399)|CUMULATIVE_LIMIT_USAGE
13:30:31.7 (7420399)|LIMIT_USAGE_FOR_NS|(default)|
  Number of SOQL queries: 0 out of 100
  Number of query rows: 0 out of 50000
  Number of SOSL queries: 0 out of 20
  Number of DML statements: 0 out of 150
  Number of DML rows: 0 out of 10000
  Maximum CPU time: 0 out of 10000
  Maximum heap size: 0 out of 6000000
  Number of callouts: 0 out of 100
  Number of Email Invocations: 0 out of 10
  Number of future calls: 0 out of 50
  Number of queueable jobs added to the queue: 0 out of 50
  Number of Mobile Apex push calls: 0 out of 10

13:30:31.7 (7420399)|CUMULATIVE_LIMIT_USAGE_END

13:30:31.6 (7446830)|CODE_UNIT_FINISHED|execute_anonymous_apex
13:30:31.6 (8089654)|EXECUTION_FINISHED
```

# Tips
`String.equals()`は大文字・小文字を`区別しません`。
大文字・小文字を区別したい場合は`if (IdA == IdB)`