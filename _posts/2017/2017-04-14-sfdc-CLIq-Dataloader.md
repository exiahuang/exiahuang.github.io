---
categories:
- Salesforce
date: 2017-04-14 22:07:34
description: SFDC CLiq Dataloader.The Salesforce Data Loader Command Line Interface
  (CLI) is a powerful tool for automating business processes, and integrating Salesforce
  with other systems. However, configuring the CLI is daunting, especially for first-time
  users. CLI quickstart (CLIq) is the solution!
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: SFDC CLiq Dataloader
update_date: 2020/05/23 23:56:51

---

# Introduction


<a target="_blank" class="btn" href="https://code.google.com/archive/p/dataloadercliq/">CLiq Dataloader Home page</a>

<div class="note primary">The Salesforce Data Loader Command Line Interface (CLI) is a powerful tool for automating business processes, and integrating Salesforce with other systems. However, configuring the CLI is daunting, especially for first-time users. CLI quickstart (CLIq) is the solution!</div>


# Config 

## Cliq Projcet Dir

```dos
C:\Cliq_DATALOADER
│   dataloader-37.0.0-uber.jar  ............ dataloader jar package
│
├─cliq_process
|   \---Sandbox                 ............ Your project
|       |   Sandbox.bat
|       |   Sandbox.sh
|       |   
|       +---config
|       |       config.properties
|       |       log-conf.xml
|       |       process-conf.xml   ......... Main Config File
|       |       Sandbox.sdl     ............ Filed Map Filed
|       |       
|       +---log
|       +---read
|       |       Sandbox.csv    ............ insert,update,upsert,delete csv
|       |       
|       \---write
|
└─Java                              ............ jdk8
    ├─bin
    │  ├─client
    │  ├─dtplugin
    │  └─plugin2
    └─lib
        ├─applet
        ├─cmm
        ├─deploy
        ├─ext
        ├─fonts
        ├─i386
        ├─images
        │  └─cursors
        ├─jfr
        ├─management
        └─security
```


## process-conf.xml Config file

`process-conf.xml` is auto created by Cliq.

```xml
<!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN//EN" "http://www.springframework.org/dtd/spring-beans.dtd">
<beans>
	<bean id="Sandbox" class="com.salesforce.dataloader.process.ProcessRunner" singleton="false">
		<description>Created by Dataloader Cliq.</description>
		<property name="name" value="Sandbox"/>
		<property name="configOverrideMap">
			<map>
				<entry key="dataAccess.name" value="C:\Cliq_DATALOADER\cliq_process\Sandbox\read\Sandbox.csv"/>
				<entry key="dataAccess.readUTF8" value="false"/>
				<entry key="dataAccess.type" value="csvRead"/>
				<entry key="dataAccess.writeUTF8" value="false"/>
				<entry key="process.enableExtractStatusOutput" value="true"/>
				<entry key="process.enableLastRunOutput" value="true"/>
				<entry key="process.lastRunOutputDirectory" value="C:\Cliq_DATALOADER\cliq_process\Sandbox\log"/>
				<entry key="process.mappingFile" value="C:\Cliq_DATALOADER\cliq_process\Sandbox\config\Sandbox.sdl"/>
				<entry key="process.operation" value="update"/>
				<entry key="process.statusOutputDirectory" value="C:\Cliq_DATALOADER\cliq_process\Sandbox\log"/>
				<entry key="sfdc.bulkApiCheckStatusInterval" value="5000"/>
				<entry key="sfdc.bulkApiSerialMode" value="5000"/>
				<entry key="sfdc.debugMessages" value="false"/>
				<entry key="sfdc.enableRetries" value="true"/>
				<entry key="sfdc.endpoint" value="https://test.salesforce.com/services/Soap/u/37.0"/>
				<entry key="sfdc.entity" value="Contact"/>
				<entry key="sfdc.extractionRequestSize" value="500"/>
				<entry key="sfdc.insertNulls" value="false"/>
				<entry key="sfdc.loadBatchSize" value="100"/>
				<entry key="sfdc.maxRetries" value="3"/>
				<entry key="sfdc.minRetrySleepSecs" value="2"/>
				<entry key="sfdc.noCompression" value="false"/>
				<entry key="sfdc.password" value="Encryption password"/>
				<entry key="sfdc.proxyHost" value=""/>
				<entry key="sfdc.proxyNtlmDomain" value=""/>
				<entry key="sfdc.proxyPassword" value="xxxxxxxxxxx"/>
				<entry key="sfdc.proxyPort" value=""/>
				<entry key="sfdc.proxyUsername" value=""/>
				<entry key="sfdc.timeoutSecs" value="60"/>
				<entry key="sfdc.useBulkApi" value="false"/>
				<entry key="sfdc.username" value="your email "/>
			</map>
		</property>
	</bean>
</beans>

```

## Sandbox.sdl

You can use dataloader to create `Sandbox.sdl` file