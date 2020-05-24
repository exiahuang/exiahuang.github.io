---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:14:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でSalesforce組織の添付ファイルを一括ダウンロードする
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:54

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってSalesforce組織の添付ファイルを一括ダウンロードする

# Attachment
User が親オブジェクトにアップロードおよび添付したファイルをダウンロードする。
`Body`をファイルに保存すれば、完了です。

# Salesforce組織の添付ファイルを一括ダウンロードする

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

SAVE_DIR = './attachments_download'
if not os.path.exists(SAVE_DIR):
    os.mkdir(SAVE_DIR)

rest_api = RestApi(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )

attachments = rest_api.query("SELECT Id, Name, Body FROM Attachment LIMIT 2000")
print("添付ファイル件数 : " + str(len(attachments)))

for attachment in attachments["records"]:
    print("start to download : " + attachment["Name"])
    """
    Run Rest API : download attachment
    """
    rest_path = "/services/data/v42.0/sobjects/Attachment/{id}/Body".format(id=attachment["Id"])
    result = rest_api.call_rest(
        method='GET',
        path=rest_path, 
        params={},
    )
    with open(os.path.join(SAVE_DIR, attachment["Id"] + "_" + attachment["Name"]), mode='wb') as f:
        f.write(result.content)
```

実行すれば、添付ファイル件数ファイルをダウンロードする可能です。