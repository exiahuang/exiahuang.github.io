---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:04:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でApexログを取得
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってApexログを取得



# Apexログを取得

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

"""get apex log"""
log_id = '07LXXXXXXXXXXXXXXXXXXXX'
result = tooling_api.getLog(log_id)
pprint.pprint(result)

```