---
categories:
- SalesforceXyToolsCore-JP
date: 2018/11/03 22:01:00
layout: post
tags:
- SalesforceXyToolsCore-JP
- salesforce
- sfdc
- python
title: SalesforcexytoolsCore Introduce
typora-copy-images-to: images/SalesforceXyToolsCore_images/
typora-root-url: ./
update_date: 2020/05/23 23:56:53

---

# Introduce
> SalesforcexytoolsCore is a python library for salesforce. It is base on [simple-salesforce](https://github.com/simple-salesforce/simple-salesforce)

* Sobject Record Management : sobject create, get, get_by_custom_id, update, delete
* Sobject Queries : query, query_more, search, query_allsearch
* Sobject Bulk action
* Run Apex Script
* Metadata Control : describeMetadata, listAllMetadata, getAllMetadataMap, listmeta, listFolder, retrieve, etc.
* Package.xml builder.
* Retrieve Metadata to memory, Retrieve Metadata zip file.
* ApexClass, Trigger, ApexComponent, ApexPage: create, update, delete, get
* Get Apex Log 
* Run test class

# Requirement
* Python3
* [requests](http://requests-docs-ja.readthedocs.io/en/latest/)

# Install
```
pip install SalesforcexytoolsCore
```

# Document
[SalesforceXyToolsCore JP Document](http://salesforcexytools.com/categories/SalesforceXyToolsCore-JP/)


# Download PDF
[SalesforcexytoolsCore-python-library-for-salesforce(日本語).pdf](http://salesforcexytools.com/pdf/SalesforceXyToolsCore-Python-Library-For-salesforce-jp.pdf)


# About Author : Exia.Huang

* [SalesforceXyTools HP](http://salesforcexytools.com)
* [Github](https://github.com/exiahuang)
* [Twitter](https://twitter.com/ExiaSfdc)
* [Facebook](https://www.facebook.com/profile.php?id=100015890262852)
* [Qiita](https://qiita.com/exiasfdc)
* [Hatenaはてなブログ](https://exiasfdc.hatenablog.com/)


# Sample Source
[Sample Source](https://github.com/exiahuang/SalesforceXyToolsCore/tree/master/example)

```
apexclass-create.py
apexclass-delete.py
apexclass-update.py
apexcomponent-create.py
build-package-xml.py
config.py
describe-metadata.py
download-attachments.py
get-all-metadata-map.py
get-apexlog.py
list-all-metadata.py
list-folders.py
list-metadata.py
package-type-list.py
retrieve-metadata-to-memory.py
retrieve-metadata-to-zip.py
run-apex-script.py
run-rest-api.py
run-soql-queries.py
run-testclass.py
sobject-CURD.py
trigger-create.py
visualforce-create.py
```