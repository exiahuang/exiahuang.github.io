---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:02:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でApexClassを作成・更新・削除
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってApexClassを作成・更新・削除



# ApexClassの作成

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

tooling_api = ToolingApi(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )

"""createApexClass"""
name = "HelloWorld"
body = """public class HelloWorld {
        private String mystr;
}"""


status_code, result = tooling_api.createApexClass(name, body)
print(status_code)
pprint.pprint(result)
```



結果確認：

```json
{'errors': [], 'id': '01pxxxxxxxxxxxxxxxxx', 'success': True}
```



# ApexClassの更新

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

tooling_api = ToolingApi(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )

apexclass_id = "set your apex class id"
body = """public class HelloWorld {
        private String mystr1;
}"""
tooling_api.updateApexClass(apexclass_id, body)
```



# ApexClassの削除

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

tooling_api = ToolingApi(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )

apexclass_id = "set your apex class id"
body = """public class HelloWorld {
        private String mystr1;
}"""
tooling_api.updateApexClass(apexclass_id, body)
```



# その他

## Triggerの作成

```python
"""createTrigger"""
tooling_api.createTrigger(tableEnumOrId, name, body)
```


## VisualForceの作成

```python
"""createApexPage"""
tooling_api.createApexPage(MasterLabel, name, markup)
```


## ApexComponentの作成

```python
"""createApexComponent"""
tooling_api.createApexComponent(MasterLabel, name, markup)
```