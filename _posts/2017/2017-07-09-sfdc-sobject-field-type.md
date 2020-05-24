---
categories:
- Salesforce
date: 2017-07-09 08:01:34
description: Salesforce Sobject Field Type
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Sobject Field Type
update_date: 2020/05/23 23:56:52

---

# Salesforce categoreis the field in three parts -
1) Read Only Fields : (auto number field, formula, rollup)
2) Relation ship Fields : ( Lookup & Master detail)
3) General Fields : ( Number, text, phone, email...etc)

Lookup field is a part of Relationship Field. Like in normal database we using foreign key in 2nd table for relate two Tables. As like same in salesforce we are using LOOKUP field or MASTER DETAIL field for making relation ship between two objects. 

Which Field we need to use for making relationship its our choice. according to our requirements we create lookup / masterdetail fields. 


## Master-detail relationship
- in m-d relationship field value is mandatory
- here parent record is deleted automatically child records is deleted
- an object is allowed only 2 m-d relationship fields
- if we give any rules to parent that rules automatically goes to the child. Child does not conatin any - seperate rules.
- we can directly conert m-d relationship to lookup relationship

`*m-d=Master-detail`

## Lookup relationship
- in lookup relationship field value is not mandatory
- here parent record is deleted automatically child records are not deleted
- an object is allowed only 25  relationship fields
- here parent rules and child rules are may be same or not.
- if we cannot give a value to the lookup field then we can't  directly conert lookup relationship to master-detail relationship here first we need to give a value to the lookup field.