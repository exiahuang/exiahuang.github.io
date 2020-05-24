---
categories:
- SalesforcexytoolsForSublime
date: 2018/10/27 22:00:01
layout: post
postman-category:
- SalesforcexytoolsForSublime
postman-tag:
- SalesforcexytoolsForSublime
- mytools
- salesforce
- sfdc
tags:
- SalesforcexytoolsForSublime
- mytools
- salesforce
- sfdc
title: How to Install SalesforceXytoolsForSublime
typora-copy-images-to: images/xytools_images
typora-root-url: ./
update_date: 2020/05/23 23:56:51

---

# SalesforceXytoolsForSublime

[SalesforceXytoolsForSublime](http://salesforcexytools.com/categories/SalesforcexytoolsForSublime/) is Rapid development tools for Salesforce Development.

- Create Salesforce Project, Retrieve Metadata, Search Metadata

- Create ApexClass, ApexTrigger, ApexComponent, Refresh, Diff with Server(Support winmerge diff), Save to Server, Deploy to Server

- SObject Viewer, SObject Description, Export SOjbect Fields to Excel

- Run SOQL Query, Tooling Query, Apex Script.

- Code Creator : Auto Create Apex Test Class Code, Auto Create Test Data For Apex Test Class.

- SFDC Dataviewer, SFDC Online Dataviewer.

- Atuo Login SFDC (two login type: oauth2 , password config).

- Quick local sfdc file from sublime.

- Quick Search SObject Data/SObject Setting/ApexClass/Trigger/VisualForce Page/VisualForce Components/Email Template/Static Resource and open on browser Quickly

- Package.xml Builder.

- Build Release Package.

- Integrate Sfdc Dataloader, Config DataLoader and Run (**Need Ant and Java Environment**)

  **Set your schedule, backup your sfdc data.**

- Integrate Sfdc Migration Tool (**Need Ant and Java Environment**)

- Auto Backup all metadata script(**Set your schedule, backup your sfdc metadata.**).




# How to Install

## Prerequisites

- Sublime Text 3 <http://www.sublimetext.com/3>
- Sublime Text Package Control <https://packagecontrol.io/installation>

## Use Package Control to Install

1. Open Sublime Text 3
2. Run `Package Control: Install Package` command

1. - [Running commands from Sublime Text](http://docs.sublimetext.info/en/latest/extensibility/command_palette.html)
     [![SalesforceXyToolsForSublimeHelp](http://salesforcexytools.com/images/salesforcexytools-for-sublime/install1.jpg)](http://salesforcexytools.com/images/salesforcexytools-for-sublime/install1.jpg)
2. Search for `SalesforceXyTools`
   [![SalesforceXyToolsForSublimeHelp](http://salesforcexytools.com/images/salesforcexytools-for-sublime/install2.jpg)](http://salesforcexytools.com/images/salesforcexytools-for-sublime/install2.jpg)
3. Hit `Enter`, That is all.
   [![SalesforceXyToolsForSublimeHelp](http://salesforcexytools.com/images/salesforcexytools-for-sublime/install3.jpg)](http://salesforcexytools.com/images/salesforcexytools-for-sublime/install3.jpg)



# Suggestion

If you want to use `ant-dataloader` or `ant-migration tools`, I suggest you to install `java` and `ant`

## Install java

just install it...

Please set your `JAVA_HOME`

## Installing Apache Ant

[Installing Apache Ant](https://ant.apache.org/manual/install.html)

To get up and running with the binary distribution of Ant quickly, follow these steps:

1. Make sure you have a Java environment installed. See [System Requirements](https://ant.apache.org/manual/install.html#sysrequirements) for details.
2. Download Ant. See [Binary Distribution](https://ant.apache.org/manual/install.html#getBinary) for details.
3. Uncompress the downloaded file into a directory.
4. Set environmental variables: `JAVA_HOME` to your Java environment, `ANT_HOME` to the directory you uncompressed Ant to, and add ${ANT_HOME}/bin (Unix) or %ANT_HOME%/bin (Windows) to your `PATH`. See [Setup](https://ant.apache.org/manual/install.html#setup) for details.
5. Optionally, from the `ANT_HOME` directory run ant -f fetch.xml -Ddest=system to get the library dependencies of most of the Ant tasks that require them. If you don't do this, many of the dependent Ant tasks will not be available. See [Optional Tasks](https://ant.apache.org/manual/install.html#optionalTasks) for details and other options for the -Ddest parameter.
6. Optionally, add any desired Antlibs. See [Ant Libraries](https://ant.apache.org/antlibs/proper.html) for a list.