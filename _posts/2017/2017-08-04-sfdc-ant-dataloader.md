---
categories:
- Salesforce
date: 2017-08-04 08:00:34
description: Salesforce Ant Dataloader backup
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Ant Dataloader backup
update_date: 2020/05/23 23:56:51

---

# template-process-conf.xml
このファイルはDataloaderのprocess-conf.xml作成するためのテンプレートです。
ANT Scriptでファイル中のパラメータを置換すると、プロセス用のprocess-conf.xmlが動的に作成されます。
```xml
<!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN//EN" "http://www.springframework.org/dtd/spring-beans.dtd">
<beans>
    <bean id="_object_" class="com.salesforce.dataloader.process.ProcessRunner" singleton="false">
    <description>Extract SFDC SObject data to CSV file.</description>
    <property name="name" value="ExtractSFDCData"/>
    <property name="configOverrideMap">
    <map>
        <entry key="sfdc.loadBatchSize" value="200"/>
        <entry key="sfdc.timeoutSecs" value="600"/>
        <entry key="dataAccess.type" value="csvWrite"/>
        <entry key="dataAccess.writeUTF8" value="true"/>
        <entry key="process.operation" value="extract"/>
        <entry key="sfdc.extractionRequestSize" value="500"/>
        <entry key="sfdc.entity" value="_object_"/>
        <entry key="sfdc.extractionSOQL" value="_soql_"/>
        <entry key="dataAccess.name" value="_file_"/>
    </map>
    </property>
    </bean>
</beans>
```
_object_は対象オブジェクト
_soql_はデータエクスポート用のSOQL
_file_は出力ファイルのフォルダーとファイル名
※設定パラメータの一覧はこちらです。

# build.xml
ANTを実行するbuild.xmlです。
このファイルで定義し、動きはまずprocess-conf.xmlを作成、そしてDataloaderのProcessRunnerを実行します。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="Export" default="all">
    <tstamp>
        <format property="today" pattern="yyyy:MM:dd"/>
    </tstamp>
    <macrodef name="export">
        <attribute name="file"/>
        <attribute name="object"/>
        <attribute name="soql"/>
        <sequential>
            <echo message="Exporting @{object}"/>
            <mkdir dir="Export_${today}"/>
            <copy 
                file="template-process-conf.xml" 
                tofile="process-conf.xml" 
                overwrite="true" 
                failonerror="true"/>
            <replace file="process-conf.xml">
                <replacefilter token="_object_" value="@{object}"/>
                <replacefilter token="_soql_" value="@{soql}"/>
                <replacefilter token="_file_" value="Export_${today}/@{file}_${today}.csv"/>
            </replace>
            <java 
                classname="com.salesforce.dataloader.process.ProcessRunner" 
                classpath="/path/to/DataLoader.jar" 
                failonerror="true">
                <sysproperty key="salesforce.config.dir" value="/path/to/config/dir"/>
                <arg line="process.name=@{object}"/>
            </java>
        </sequential>
    </macrodef>
    <target name="all">
        <export file="Account" object="Account" soql="Select Id, Name From Account LIMIT 10"/>
        <export file="Contact" object="Contact" soql="Select Id, Name From Contact LIMIT 10"/>
    </target>
</project>
```

<tstamp> は今日の期日のプロパティを取得します
<macrodef>の<attribute> はファイル、オブジェクト、SOQLの属性です
<copy> はtemplate-process-conf.xmlからprocess-conf.xmlを作成します
<replace> はprocess-conf.xmlファイルに対してパラメータを置換します
<java> はDataloaderのプログラムを実行します
「classpath」はDataLoader.jarのインストール先のパスで、例えばMacのLexiLoader v30なら”/Applications/LexiLoader_v30.app/Contents/Resources/Java/DataLoader.jar”になるはずです
「salesforce.config.dir」プロパティはログイン情報を保存するconfig.propertiesファイルが格納されているディレクトリのパスです
<target> は処理対象の属性を定義します。従来の使い方では一対象一コンフィグファイルですが、これにより処理対象の差分属性のみ、一つのところで管理できます
コマンドラインで「ant all」を実行すると「all」の中で定義したtargetのマクロを順番で実行します。

手入力条件について、<sequential>の中の<input>を使って手入力値も引数として処理されます。
下の例では、入力した値をwhereプロパティとしてSOQLにつけ加えます。

<input message="Enter WHERE Condition, example: WHERE Type = 'Person'" addproperty="where" />
<replace file="process-conf.xml">
    <replacefilter token="_soql_" value="@{soql} ${where}"/>
</replace>

今回はエクスポートの場合をご紹介していますが、もちろんインポートもできます。インポート用のマッピングファイルもパラメータとして処理できます。

# template-process-conf.xml

```xml
<entry key="process.mappingFile"  value="_mappingFile_"/>
```

# build.xml
```xml
<target name="all">
 　　　<insert file="Account" object="Account" mappingFile="AccountFieldMapping.sdl"/>
</target>
```
 
# 最後に
定期的にプロセスをやると、ユニックスのcrontabやウィンドウズのタスクスケジューラなどのスケジュールツールを使って実行します。
以上、ANT Scriptの使用例について説明してきましたが、処理が可能な範囲はこれだけではありません、例えばreplace機能でcsvファイルの中身の更新もできます。
ANTの便利機能を使いこなしてデータプロセスを自動化しましょう。