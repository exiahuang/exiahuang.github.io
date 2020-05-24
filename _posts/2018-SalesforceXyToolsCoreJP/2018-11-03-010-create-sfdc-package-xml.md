---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:10:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforceXyToolsCore/Python上でSalesforce組織からのPackage.xmlを作成
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Topic

* [SalesforceXyToolsCore](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)を使ってSalesforce組織からのPackage.xmlを作成



# Package.xmlの作成

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


"""buildPackageXml"""
packagexml = meta_api.buildPackageXml()
```



結果確認：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">

    <types>
        <members>*</members>
        <name>InstalledPackage</name>
    </types>
    <types>
        <members>*</members>
        <name>CustomLabels</name>
    </types>
    
        ....................
        ........省略.........
        ....................
    <types>
        <members>Account</members>
        <members>AccountChangeEvent</members>
        <members>AccountCleanInfo</members>
        <members>AccountContactRole</members>
        <members>AccountFeed</members>
        <members>AccountHistory</members>
        <members>AccountPartner</members>
        <members>AccountShare</members>
        <members>ActionLinkGroupTemplate</members>
        <members>ActionLinkTemplate</members>
        <members>ActivityHistory</members>
        <members>AdditionalNumber</members>
        <members>AggregateResult</members>
        ....................
        ........省略.........
        ....................
        <name>CustomObject</name>
    </types>
    <types>
        <members>unfiled$public</members>
        ....................
        ........省略.........
        ....................
        <members>unfiled$public/SupportCaseAssignmentNotification</members>
        <members>unfiled$public/SalesNewCustomerEmail</members>
        <members>unfiled$public/SupportCaseCreatedWebInquiries</members>
        <members>unfiled$public/SupportEscalatedCaseNotification</members>
        <members>unfiled$public/SupportSelfServiceResetPassword</members>
        <members>unfiled$public/MarketingProductInquiryResponse</members>
        <members>unfiled$public/SupportCaseCreatedPhoneInquiries</members>
        <members>unfiled$public/SUPPORTSelfServiceResetPasswordSAMPLE</members>
        <members>unfiled$public/SupportEscalatedCaseReassignment</members>
        <members>unfiled$public/SUPPORTSelfServiceNewCommentNotificationSAMPLE</members>
        <name>EmailTemplate</name>
    </types>

        ....................
        ........省略.........
        ....................
    <types>
        <members>*</members>
        <name>TopicsForObjects</name>
    </types>
    <types>
        <members>*</members>
        <name>EmailServicesFunction</name>
    </types>
    <types>
        <members>*</members>
        <name>Settings</name>
    </types>
    <version>42.0</version>
</Package>


```



# SFDC組織からPackage関するリストを取得

```python
"""packageTypeList"""
print('>>>packageTypeList')
pprint.pprint(meta_api.packageTypeList())
```

結果確認
```json

[{'members': ['*'], 'name': 'InstalledPackage'},
 {'members': ['*'], 'name': 'CustomLabels'},
 {'members': ['*'], 'name': 'StaticResource'},
         ....................
        ........省略.........
        ....................
 {'members': ['*'], 'name': 'TopicsForObjects'},
 {'members': ['*'], 'name': 'EmailServicesFunction'},
 {'members': ['*'], 'name': 'Settings'}]

```