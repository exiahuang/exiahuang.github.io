---
categories:
- Salesforce
date: 2017-07-08 08:02:34
description: Salesforce Using REGEX Validations
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Using REGEX Validations
update_date: 2020/05/23 23:56:51

---

# Pagination using standardsetcontroller

As the number of records increases, the time required for the browser to render them increases. Paging is used to reduce the amount of data exchanged with the client. Paging is typically handled on the server side (standardsetcontroller). The page sends parameters to the controller, which the controller needs to interpret and then respond with the appropriate data set.

## Here is the controller which makes use of standard set controller for pagination

```java
public with sharing class Pagination {
    Public Integer noOfRecords{get; set;}
    Public Integer size{get;set;}
    public ApexPages.StandardSetController setCon {
        get{
            if(setCon == null){
                size = 10;
                string queryString = 'Select Name, Type, BillingCity, BillingState, BillingCountry from Account order by Name';
                setCon = new ApexPages.StandardSetController(Database.getQueryLocator(queryString));
                setCon.setPageSize(size);
                noOfRecords = setCon.getResultSize();
            }
            return setCon;
        }set;
    }
     
    Public List<Account> getAccounts(){
        List<Account> accList = new List<Account>();
        for(Account a : (List<Account>)setCon.getRecords())
            accList.add(a);
        return accList;
    }
     
    public pageReference refresh() {
        setCon = null;
        getAccounts();
        setCon.setPageNumber(1);
        return null;
    }
     
    public Boolean hasNext {
        get {
            return setCon.getHasNext();
        }
        set;
    }
    public Boolean hasPrevious {
        get {
            return setCon.getHasPrevious();
        }
        set;
    }
  
    public Integer pageNumber {
        get {
            return setCon.getPageNumber();
        }
        set;
    }
  
    public void first() {
        setCon.first();
    }
  
    public void last() {
        setCon.last();
    }
  
    public void previous() {
        setCon.previous();
    }
  
    public void next() {
        setCon.next();
    }
}
```

Using the above controller methods we can define the pagination.

```jsp
<apex:page controller="Pagination">
    <apex:form >
        <apex:pageBlock id="pb">
            <apex:pageBlockTable value="{!Accounts}" var="a">
                <apex:column value="{!a.Name}"/>
                <apex:column value="{!a.Type}"/>
                <apex:column value="{!a.BillingCity}"/>
                <apex:column value="{!a.BillingState}"/>
                <apex:column value="{!a.BillingCountry}"/>
            </apex:pageBlockTable>
            <apex:panelGrid columns="7">
                <apex:commandButton status="fetchStatus" reRender="pb" value="|<" action="{!first}" disabled="{!!hasPrevious}" title="First Page"/>
                <apex:commandButton status="fetchStatus" reRender="pb" value="<" action="{!previous}" disabled="{!!hasPrevious}" title="Previous Page"/>
                <apex:commandButton status="fetchStatus" reRender="pb" value=">" action="{!next}" disabled="{!!hasNext}" title="Next Page"/>
                <apex:commandButton status="fetchStatus" reRender="pb" value=">|" action="{!last}" disabled="{!!hasNext}" title="Last Page"/>
                <apex:outputText >{!(pageNumber * size)+1-size}-{!IF((pageNumber * size)>noOfRecords, noOfRecords,(pageNumber * size))} of {!noOfRecords}</apex:outputText>
                <apex:commandButton status="fetchStatus" reRender="pb" value="Refresh" action="{!refresh}" title="Refresh Page"/>
                <apex:outputPanel style="color:#4AA02C;font-weight:bold">
                    <apex:actionStatus id="fetchStatus" startText="Fetching..." stopText=""/>
                </apex:outputPanel>
            </apex:panelGrid>
        </apex:pageBlock>
    </apex:form>
</apex:page>
```

# minified version of controller and page

Do you really feel the code is little larger then what you expect, here is the minified version of controller and page
Controller Code:
```java
public with sharing class Pagination_min {
    Public Integer noOfRecords{get; set;}
    Public Integer size{get;set;}
    public ApexPages.StandardSetController setCon {
        get{
            if(setCon == null){
                size = 10;
                string queryString = 'Select Name, Type, BillingCity, BillingState, BillingCountry from Account order by Name';
                setCon = new ApexPages.StandardSetController(Database.getQueryLocator(queryString));
                setCon.setPageSize(size);
                noOfRecords = setCon.getResultSize();
            }
            return setCon;
        }set;
    }
     
    Public List<Account> getAccounts(){
        List<Account> accList = new List<Account>();
        for(Account a : (List<Account>)setCon.getRecords())
            accList.add(a);
        return accList;
    }
     
    public pageReference refresh() {
        setCon = null;
        getAccounts();
        setCon.setPageNumber(1);
        return null;
    }
}
```

Page Code:
```jsp
<apex:page controller="Pagination_min">
    <apex:form >
        <apex:pageBlock id="pb">
            <apex:pageBlockTable value="{!Accounts}" var="a">
                <apex:column value="{!a.Name}"/>
                <apex:column value="{!a.Type}"/>
                <apex:column value="{!a.BillingCity}"/>
                <apex:column value="{!a.BillingState}"/>
                <apex:column value="{!a.BillingCountry}"/>
            </apex:pageBlockTable>
            <apex:panelGrid columns="7">
                <apex:commandButton status="fetchStatus" reRender="pb" value="|<" action="{!setCon.first}" disabled="{!!setCon.hasPrevious}" title="First Page"/>
                <apex:commandButton status="fetchStatus" reRender="pb" value="<" action="{!setCon.previous}" disabled="{!!setCon.hasPrevious}" title="Previous Page"/>
                <apex:commandButton status="fetchStatus" reRender="pb" value=">" action="{!setCon.next}" disabled="{!!setCon.hasNext}" title="Next Page"/>
                <apex:commandButton status="fetchStatus" reRender="pb" value=">|" action="{!setCon.last}" disabled="{!!setCon.hasNext}" title="Last Page"/>
                <apex:outputText >{!(setCon.pageNumber * size)+1-size}-{!IF((setCon.pageNumber * size)>noOfRecords, noOfRecords,(setCon.pageNumber * size))} of {!noOfRecords}</apex:outputText>
                <apex:commandButton status="fetchStatus" reRender="pb" value="Refresh" action="{!refresh}" title="Refresh Page"/>
                <apex:outputPanel style="color:#4AA02C;font-weight:bold">
                    <apex:actionStatus id="fetchStatus" startText="Fetching..." stopText=""/>
                </apex:outputPanel>
            </apex:panelGrid>
        </apex:pageBlock>
    </apex:form>
</apex:page>
```