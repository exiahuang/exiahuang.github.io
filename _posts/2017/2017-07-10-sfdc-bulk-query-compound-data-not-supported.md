---
categories:
- Salesforce
date: 2017-07-10 08:00:34
description: Salesforce Selecting compound data not supported in Bulk Query
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Selecting compound data not supported in Bulk Query
update_date: 2020/05/23 23:56:51

---

# Error msg
InvalidBatch : Failed to process query: FUNCTIONALITY_NOT_ENABLED: Selecting compound data not supported in Bulk Query

# Explain
There isn't much out there on this error.  Before doing any data update, I like to export the target object's full data set as a precaution.  My tool of choice is workbench but sometimes it can be a little baby and complain like "Selecting compound data not supported in Bulk Query". 

Turns out that the following fields are going to make your bulk api export fail:


`住所` Address fields like:
- Billing Address
- Shipping Address

`地理位置情報` Latitude and Longitude fields like:
- BillingLatitude
- BillingLongitude


These are your most common "compound" fields.  Once you remove these fields from your export, you should be ok.

Source: https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/compound_fields.htm