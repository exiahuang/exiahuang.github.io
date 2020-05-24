---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:06:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でSalesforce組織のSoqlを実行する
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってSalesforce組織のSoqlを実行する



# メールテンプレートのフォルダーを取得する

* Salesforce組織のユーザ名、パスワード、Apiバージョン、Product/Sandboxを設定してください。

```python
from SalesforceXytoolsCore import *
import pprint

config = {
    "api_version": 42.0, 
    "username": "sfdc username", 
    "password": "sfdc password", 
    "security_token": "", 
    "is_sandbox": True
}

soap_api = Soap(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )

"""
Run Soql Queries
"""
soql_string = "SELECT Id, Name FROM User LIMIT 3"
result = soap_api.query(soql_string)
pprint.pprint(result)


```



## 結果確認

```json
OrderedDict([('totalSize', 3),
             ('done', True),
             ('records',
              [OrderedDict([('attributes',
                             OrderedDict([('type', 'User'),
                                          ('url',
                                           '/services/data/v42.0/sobjects/User/005XXXXXXXXXXXXXXX')])),
                            ('Id', '005XXXXXXXXXXXXXXX'),
                            ('Name', 'Process Automated')]),
               OrderedDict([('attributes',
                             OrderedDict([('type', 'User'),
                                          ('url',
                                           '/services/data/v42.0/sobjects/User/005XXXXXXXXXXXXXXX')])),
                            ('Id', '005XXXXXXXXXXXXXXX'),
                            ('Name', 'サイトゲストユーザ')]),
               OrderedDict([('attributes',
                             OrderedDict([('type', 'User'),
                                          ('url',
                                           '/services/data/v42.0/sobjects/User/005XXXXXXXXXXXXXXX')])),
                            ('Id', '005XXXXXXXXXXXXXXX'),
                            ('Name', 'SFDC Exia')])])])
```



# その他方法

## query_more
```
soap_api.query_more(sobject_id)
soap_api.query_more("/services/data/v43.0/query/sobject_id", True)
```


## query_allですべてのデータを取得する
```
soap_api.query_all("SELECT Id, Email FROM Contact WHERE LastName = 'Jones'")
```

## search
```
soap_api.search("FIND {exia}")
```

## quick_search
```
soap_api.quick_search("exia")
```