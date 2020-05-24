---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:13:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でたった3行でSalesforce組織からのメタデータの取得
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:54

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってSalesforce組織からのメタデータの取得



# メリット

* package.xml配置不要、動的に生成
* すべてのSalesforce組織からのメタデータ一括で取得



# Salesforce組織からのメタデータの取得

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

meta_api = MetadataApi(username=config["username"], 
                password=config["password"], 
                security_token=config["security_token"], 
                sandbox=config["is_sandbox"],
                version=config["api_version"]
                )


"""retrieve zip file"""
meta_api.retrieveZip("./save_dir","metadata-retrieve.zip")
```



結果確認：

```
ls ./save_dir
```



# 分析

## メタデータ取得ロジック

1. retrieve() コールを発行し、非同期的な取得を開始すると、[AsyncResult](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_asyncresult.htm) オブジェクトが返されます。[id](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_asyncresult.htm#async_result_id) 項目の値をメモし、次のステップで使用します。
2. [checkRetrieveStatus()](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_checkretrievestatus.htm) コールを発行して、最初のステップの [AsyncResult](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_asyncresult.htm) オブジェクトから [id](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_asyncresult.htm#async_result_id) 値を渡します。返された [RetrieveResult](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_retrieveresult.htm#meta_retrieveresult) の [done](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_retrieveresult.htm#retrieveresult_done) 項目の値をチェックします。true の場合、コールが完了して、次のステップに進むことを意味します。それ以外の場合は、[done](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_retrieveresult.htm#retrieveresult_done) 項目が true になるまで、このステップを繰り返して [checkRetrieveStatus()](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_checkretrievestatus.htm) を再度コールします。
3. 前のステップの [checkRetrieveStatus()](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_checkretrievestatus.htm) への最後のコールで返された [RetrieveResult](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_retrieveresult.htm#meta_retrieveresult) から zip ファイル ([zipFile](https://developer.salesforce.com/docs/atlas.ja-jp.api_meta.meta/api_meta/meta_retrieveresult.htm#retrieveResult_zipFile) 項目) および他の必要な項目を取得します。



## retrieveタスクを開始

タスクを発行する

```python
"""retrieve"""
result = meta_api.startRetrieve()
pprint.pprint(result)
# print(result["done"])
# print(result["id"])
# print(result["state"])

```

## retrieveの状況を確認

宣言的なメタデータコール retrieve() の状況を確認し、zip ファイルの内容を返します。

```
"""checkRetrieveStatus"""
retrieve_id = result["id"]
check_result = meta_api.checkRetrieveStatus(retrieve_id)
pprint.pprint(check_result)

```