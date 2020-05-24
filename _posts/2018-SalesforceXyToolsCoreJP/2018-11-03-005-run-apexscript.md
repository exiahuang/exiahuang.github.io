---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:05:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でApexScriptを実行する
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってSalesforceのApexScriptを実行する





# ApexScriptを実行する

Salesforce組織のユーザ名、パスワード、Apiバージョン、Product/Sandboxを設定してください。

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
Run Apex Script
"""
apex_string = "System.debug('hello world');"
debug_levels = {
        "DB": "Info", 
        "System": "DEBUG", 
        "Workflow": "INFO", 
        "Callout": "INFO", 
        "Validation": "INFO", 
        "Apex_Code": "DEBUG", 
        "Apex_Profiling": "INFO"
    }
result = soap_api.execute_anonymous(apex_string, debug_levels)
pprint.pprint(result)
```



## 結果ログを確認：

```json
{'debugLog': '42.0 '
             'APEX_CODE,DEBUG;APEX_PROFILING,INFO;CALLOUT,INFO;DB,INFO;SYSTEM,DEBUG;VALIDATION,INFO;WORKFLOW,INFO\n'
             "Execute Anonymous: System.debug('hello world');\n"
             '22:22:14.19 '
             '()|USER_INFO|[EXTERNAL]|xxxxxxxxxxxxxxxxxxxxxxxxx|日本標準時|GMT+09:00\n'
             '22:22:14.19 ()|EXECUTION_STARTED\n'
             '22:22:14.19 '
             '()|CODE_UNIT_STARTED|[EXTERNAL]|execute_anonymous_apex\n'
             '22:22:14.19 ()|USER_DEBUG|[1]|DEBUG|hello world\n'
             '22:22:14.19 ()|CUMULATIVE_LIMIT_USAGE\n'
             '22:22:14.19 ()|LIMIT_USAGE_FOR_NS|(default)|\n'
             '  Number of SOQL queries: 0 out of 100\n'
             '  Number of query rows: 0 out of 50000\n'
             '  Number of SOSL queries: 0 out of 20\n'
             '  Number of DML statements: 0 out of 150\n'
             '  Number of DML rows: 0 out of 10000\n'
             '  Maximum CPU time: 0 out of 10000\n'
             '  Maximum heap size: 0 out of 6000000\n'
             '  Number of callouts: 0 out of 100\n'
             '  Number of Email Invocations: 0 out of 10\n'
             '  Number of future calls: 0 out of 50\n'
             '  Number of queueable jobs added to the queue: 0 out of 50\n'
             '  Number of Mobile Apex push calls: 0 out of 10\n'
             '\n'
             '22:22:14.19 ()|CUMULATIVE_LIMIT_USAGE_END\n'
             '\n'
             '22:22:14.19 '
             '()|CODE_UNIT_FINISHED|execute_anonymous_apex\n'
             '22:22:14.19 ()|EXECUTION_FINISHED\n',
 'success': True}
```