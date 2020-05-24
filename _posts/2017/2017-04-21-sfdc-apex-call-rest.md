---
categories:
- Salesforce
date: 2017-04-21 22:02:34
description: SFDC Apex Call Rest
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC Apex Call Rest
update_date: 2020/05/23 23:56:51

---

# SFDC Apex Call Rest
Use apex code to call Rest Api

```java
	RestRequest req = new RestRequest();
	req.addHeader('Content-Type', 'application/json; charset=UTF-8');
	req.requestURI = '/your_url';
	req.httpMethod = 'POST';
	req.requestBody = Blob.valueOf(JSON.serialize(new Map<String, Object>{
	    'param1' => '12345',
	    'param2' => '3456',
	    'param3'      => new List<Map<String, Object>> {
	      new Map<String, Object> {
	        'p1'     => '2',
	        'p2'    => 1
	      }
	  }
	}));

	RestContext.request = req;
	RestContext.response = new RestResponse();

	YourClass.CallPostRest();

	String body = RestContext.response.responseBody.toString();
	System.debug(body);
```


# Call Use Rest Api 
call the url `/services/apexrest/your_url` by <a target="_blank" class="btn" href="https://chrome.google.com/webstore/detail/salesforcexytools/ehklfkbacogbanjgekccnbfdgjechlmf?hl=ja">SalesforceXyTools For Chrome</a>
{
  "param1": "1",
  "param2": "2",
  "param3": {
    "p1": "3",
    "p2": 1
  }
}