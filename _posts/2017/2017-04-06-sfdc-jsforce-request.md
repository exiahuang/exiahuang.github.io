---
categories:
- Salesforce
date: 2017-04-06 22:12:34
description: How to use jsforce to call rest api?
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: How to use jsforce to call rest api?
update_date: 2020/05/23 23:56:51

---

# How to use jsforce to call rest api?

```js
    var _request = {
        url: '/services/data/v37.0/sobjects',
        method: 'get',
        body: '',
        headers : {
                "Content-Type" : "application/json"
            }
    };
    console.log(_request);

    conn.request(_request, function(err, resp) {
        console.log(resp);
    });
```

The URL for a namespaced classes contains the namespace. For example, if your class is in namespace abc and the class is mapped to your_url, then the API URL is modified as follows: `https://instance.salesforce.com/services/apexrest/abc/your_url/`. In the case of a URL collision, the namespaced class is always used.

# more help

<a target="_blank" class="btn" href="https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_annotation_rest_resource.htm">More Apex Developer Guide Help</a>