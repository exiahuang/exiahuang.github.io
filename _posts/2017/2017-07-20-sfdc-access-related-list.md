---
categories:
- Salesforce
date: 2017-07-20 08:06:34
description: How to access an object related lists in apex
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: How to access an object related lists in apex
update_date: 2020/05/23 23:56:51

---

# How to access an object related lists in apex
I have an object 'Household Served' with a field called volunteer, and it also has an Event attached to it. The Event has a related list of Contacts. I need to write a trigger that validates the the volunteer on the Household served object is in the related list of the event.

Currently I have :

```java
trigger VolunteerValidate on Household_Served__c (before insert, before update) {
    for(Household_Served__c house : Trigger.new){
        Event__c e = new Event__c();
        e.Id = house.Event__c;
        if(house.Volunteer_Name__c != e.RelatedListGoesHere){

        }
    }
}
```
How can I access the Event's related list of contacts?

# Answer
The related list of contacts can be accessed via a sub-select. I'm assuming you are using the standard Contacts object.

You want something like this (this is bulkified, btw)

- Get a list of eventids
- Query events and associated contacts. Put in a map.
- Loop through Household_Server__c
- Get related Event__c from the map.
- Loop through the contacts on the Event__c
- If one matches, you are gold.

Here is the code:
```java
Set<id> eventIds = new Set<Id>();
for (Household_Served__c house : Trigger.new) {
    eventIds.add(house.Event__c);
}
Map<Id, Event__c> eventMap = new Map<id,Event__c>([SELECT id, Name, 
                                                                   (SELECT Id, Name 
                                                                    FROM Contacts)
                                                   FROM Event__c 
                                                   WHERE id in :eventIds]);

for(Household_Served__c house : Trigger.new){
    Event__c e eventMap.get(house.Event__c);
    if (e == null){
        continue;
    }

    Boolean contactIsOnEvent = false;
    for (Contact c : e.Contacts){
        if(house.Volunteer_Name__c = c.Name){
            contactIsOnEvent = true;
        }
    }
}
```