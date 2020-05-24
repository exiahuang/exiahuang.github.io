---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:12:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でSalesforce組織のフォルダーを取得する
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってすべてのSalesforce組織のフォルダーを取得する



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

meta_api = MetadataApi(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )


"""listFolder"""
folders = meta_api.listFolder("EmailTemplate")
pprint.pprint(folders)

```



## 結果確認

```json
{'ApexClass': {'classes/A_Batch.cls': OrderedDict([('createdById',
                                                    '005xxxxxxxxxxxxx'),
                                                   ('createdByName',
                                                    'SFDC Exia'),
                                                   ('createdDate',
                                                    '2010-08-09T00:07:13.000Z'),
                                                   ('fileName',
                                                    'classes/A_Batch.cls'),
                                                   ('fullName', 'A_Batch'),
                                                   ('id', '01pxxxxxxxxxxxxx'),
                                                   ('lastModifiedById',
                                                    '005xxxxxxxxxxxxx'),
                                                   ('lastModifiedByName',
                                                    'SFDC Exia'),
                                                   ('lastModifiedDate',
                                                    '2010-08-09T00:24:29.000Z'),
                                                   ('manageableState',
                                                    'unmanaged'),
                                                   ('type', 'ApexClass')]),
               ................省略
                'Report': {
            'reports/Xy/MyID.report': OrderedDict([('createdById',
                                                    '005xxxxxxxxxxxxx'),
                                                   ('createdByName',
                                                    'SFDC Exia'),
                                                   ('createdDate',
                                                    '2010-09-15T00:29:36.000Z'),
                                                   ('fileName',
                                                    'reports/Xy/MyID.report'),
                                                   ('fullName', 'Xy/MyID'),
                                                   ('id', '00OXXXXXXXXXXXXXX'),
                                                   ('lastModifiedById',
                                                    '005XXXXXXXXXXXXXX'),
                                                   ('lastModifiedByName',
                                                    'SFDC Exia'),
                                                   ('lastModifiedDate',
                                                    '2010-09-25T00:03:33.000Z'),
                                                   ('manageableState',
                                                    'unmanaged'),
                                                   ('type', 'Report')]),
               ................省略
}

```



# その以外のフォルダー

Salesforce には、現在次の 4 つのフォルダの種類があります。

- ドキュメントフォルダ
- メールフォルダ
- レポートフォルダ
- ダッシュボードフォルダ



Four folder types currently exist in Salesforce:

- Document folder
- Email folder
- Report folder
- Dashboard folder



取得方法：

```python
"""Email folderの取得"""
folders = meta_api.listFolder("EmailTemplate")

"""Document folderの取得"""
folders = meta_api.listFolder("Document")

"""Report folderの取得"""
folders = meta_api.listFolder("Report")

"""Dashboard folderの取得"""
folders = meta_api.listFolder("Dashboard")


```