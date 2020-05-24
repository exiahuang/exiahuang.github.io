---
categories:
- Salesforce
date: 2017-07-08 08:08:34
description: Salesforce one-to-one relationship
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce one-to-one relationship
update_date: 2020/05/23 23:56:51

---

# How can i create one-to-one relationship between two custom objects in salesforce.com. 
 
Example: I have two custom objects having following details:
 
1) Employee (Name, PanCardNo)
2)PanCard(PanCardNo Name_on_card)
 
I have gone through documents of salesforce, but i can able to find out only lookup (One-to-many raltionship) and master-detail relationship(many-to-many relationship).
 
Is there any way to create one-to-one relationship??

# Types of relationships that Salesforce provide
- `Master-detail relationship`　主従関係
- `Lookup` 参照関係

# Creating one to one relationship between objects in Salesforce
## Solution
In this article we'll be using Master-detail relationship to implement `one-to-one` relationship.

To make a this relationship one-to-one we will be using `rollup` summary concept.
1. Create a rollup summary field `managerCount` (count)  in departments, this will be auto populated depending upon the number of managers associated with that particular department.
2. Create a `validation rule`(`入力規則`) in department object on managerCount field. Throw an error "department can be managed by only one manager"when the managerCount is greater that 1.