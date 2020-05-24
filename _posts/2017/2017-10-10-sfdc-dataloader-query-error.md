---
categories:
- Salesforce
date: 2017-10-10 08:02:34
description: Salesforce Dataloader Exception
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Dataloader Exception
update_date: 2020/05/23 23:56:51

---

# summary
please exclude salesforce object below:

- AttachedContentDocument
- ContractStatus
- SolutionStatus
- TaskPriority
- NoteAndAttachment
- FolderedContentDocument
- TaskStatus
- ContentFolderItem
- CaseStatus
- OpenActivity
- RecentlyViewed
- ProcessInstanceHistory
- ActivityHistory
- FlexQueueItem
- PartnerRole
- EmailStatus
- UserRecordAccess
- DeclinedEventRelation
- AcceptedEventRelation
- UndecidedEventRelation
- DatacloudAddress



# Dataloader not support Sobject
- AttachedContentDocument
- ContractStatus
- SolutionStatus
- TaskPriority
- NoteAndAttachment
- FolderedContentDocument
- TaskStatus
- ContentFolderItem
- CaseStatus
- OpenActivity
- RecentlyViewed
- ProcessInstanceHistory
- ActivityHistory
- FlexQueueItem
- PartnerRole
- EmailStatus
- UserRecordAccess
- DeclinedEventRelation
- AcceptedEventRelation
- UndecidedEventRelation
- DatacloudAddress
- EntityParticle
- SearchLayout
- UserEntityAccess
- RelationshipInfo
- OwnerChangeOptionInfo
- RelationshipDomain
- PicklistValueInfo
- IdeaComment
- CollaborationGroupRecord
- UserFieldAccess
- ContentFolderMember
- FieldDefinition
- ContentDocumentLink
- Vote
- ContentHubItem
- FlexQueueItem
- ListViewChartInstance
- DataStatistics
- PlatformAction



If you add them, Dataloader Exception will be like below
```
2017-10-10 04:36:10,412 ERROR [PartnerRole] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Entity 'PartnerRole' is not supported by the Bulk API.
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:91)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
Caused by: [AsyncApiException  exceptionCode='InvalidEntity'
 exceptionMessage='Entity 'PartnerRole' is not supported by the Bulk API.'
]

	at com.sforce.async.BulkConnection.parseAndThrowException(BulkConnection.java:180)
	at com.sforce.async.BulkConnection.createOrUpdateJob(BulkConnection.java:164)
	at com.sforce.async.BulkConnection.createOrUpdateJob(BulkConnection.java:132)
	at com.sforce.async.BulkConnection.createJob(BulkConnection.java:122)
	at com.salesforce.dataloader.action.visitor.BulkApiVisitorUtil.createJob(BulkApiVisitorUtil.java:114)
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:68)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	... 6 more
2017-10-10 04:36:10,413 ERROR [PartnerRole] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Entity 'PartnerRole' is not supported by the Bulk API.
```


# is not supported by the Bulk API, Not Queryable

- ActivityHistory
- AggregateResult
- AttachedContentDocument
- AttachedContentNote
- CombinedAttachment
- EmailStatus
- FeedLike
- FeedTrackedChange
- FolderedContentDocument
- LookedUpFromActivity
- Name
- NoteAndAttachment
- OpenActivity
- OwnedContentDocument
- ProcessInstanceHistory
- QuoteTemplateRichTextData

you can use queryable field to check this

```
2017-10-10 04:55:24,650 ERROR [Name] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Entity 'Name' is not supported by the Bulk API.
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:91)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
Caused by: [AsyncApiException  exceptionCode='InvalidEntity'
 exceptionMessage='Entity 'Name' is not supported by the Bulk API.'
]

	at com.sforce.async.BulkConnection.parseAndThrowException(BulkConnection.java:180)
	at com.sforce.async.BulkConnection.createOrUpdateJob(BulkConnection.java:164)
	at com.sforce.async.BulkConnection.createOrUpdateJob(BulkConnection.java:132)
	at com.sforce.async.BulkConnection.createJob(BulkConnection.java:122)
	at com.salesforce.dataloader.action.visitor.BulkApiVisitorUtil.createJob(BulkApiVisitorUtil.java:114)
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:68)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	... 6 more
2017-10-10 04:55:24,651 ERROR [Name] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Entity 'Name' is not supported by the Bulk API.
```

# Failed to process query: MALFORMED_QUERY: EntityParticle: 列を絞り込む場合、条件は必須です
関連オブジェクト

- EntityParticle
- SearchLayout
- UserEntityAccess
- RelationshipInfo
- OwnerChangeOptionInfo
- RelationshipDomain
- PicklistValueInfo
- IdeaComment
- CollaborationGroupRecord
- UserFieldAccess
- ContentFolderMember
- FieldDefinition
- ContentDocumentLink
- Vote
- ContentHubItem


```
2017-10-10 05:40:33,946 ERROR [EntityParticle] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: EntityParticle: 列を絞り込む場合、条件は必須です [EntityDefinitionId,FieldDefinitionId,DurableId]
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:76)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
2017-10-10 05:40:33,948 ERROR [EntityParticle] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: EntityParticle: 列を絞り込む場合、条件は必須です [EntityDefinitionId,FieldDefinitionId,DurableId]


....
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: EntityParticle: 列を絞り込む場合、条件は必須です [EntityDefinitionId,FieldDefinitionId,DurableId]
2017-10-10 04:33:59,058 ERROR [EntityParticle] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: EntityParticle: 列を絞り込む場合、条件は必須です [EntityDefinitionId,FieldDefinitionId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: SearchLayout: 列を絞り込む場合、条件は必須です [EntityDefinitionId,DurableId]
2017-10-10 04:41:12,490 ERROR [SearchLayout] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: SearchLayout: 列を絞り込む場合、条件は必須です [EntityDefinitionId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: UserEntityAccess: 列を絞り込む場合、条件は必須です [UserId,DurableId]
2017-10-10 04:41:57,171 ERROR [UserEntityAccess] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: UserEntityAccess: 列を絞り込む場合、条件は必須です [UserId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: RelationshipInfo: 列を絞り込む場合、条件は必須です [ChildSobjectId,FieldId,DurableId]
2017-10-10 04:42:02,755 ERROR [RelationshipInfo] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: RelationshipInfo: 列を絞り込む場合、条件は必須です [ChildSobjectId,FieldId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: OwnerChangeOptionInfo: 列を絞り込む場合、条件は必須です [EntityDefinitionId,DurableId]
2017-10-10 04:44:33,744 ERROR [OwnerChangeOptionInfo] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: OwnerChangeOptionInfo: 列を絞り込む場合、条件は必須です [EntityDefinitionId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: RelationshipDomain: 列を絞り込む場合、条件は必須です [ParentSobjectId,ChildSobjectId,FieldId,RelationshipInfoId,DurableId]
2017-10-10 04:46:50,032 ERROR [RelationshipDomain] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: RelationshipDomain: 列を絞り込む場合、条件は必須です [ParentSobjectId,ChildSobjectId,FieldId,RelationshipInfoId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: PicklistValueInfo: 列を絞り込む場合、条件は必須です [EntityParticleId,DurableId]
2017-10-10 04:48:12,019 ERROR [PicklistValueInfo] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: PicklistValueInfo: 列を絞り込む場合、条件は必須です [EntityParticleId,DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction. When querying the Idea Comment object, you must filter using the following syntax: CommunityId = [single ID], Id = [single ID], IdeaId = [single ID], Id IN [list of IDs], or IdeaId IN [list of IDs].
2017-10-10 04:48:34,697 ERROR [IdeaComment] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction. When querying the Idea Comment object, you must filter using the following syntax: CommunityId = [single ID], Id = [single ID], IdeaId = [single ID], Id IN [list of IDs], or IdeaId IN [list of IDs].
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: 実装の制限: CollaborationGroupRecord では、等号を使用した単一 ID、CollaborationGroupId または RecordId による絞り込み条件が必要です。
2017-10-10 04:48:57,929 ERROR [CollaborationGroupRecord] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: 実装の制限: CollaborationGroupRecord では、等号を使用した単一 ID、CollaborationGroupId または RecordId による絞り込み条件が必要です。
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: UserFieldAccess: 列を絞り込む場合、条件は必須です [DurableId]
2017-10-10 04:49:07,749 ERROR [UserFieldAccess] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: UserFieldAccess: 列を絞り込む場合、条件は必須です [DurableId]
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction: ContentFolderMember requires a filter by a single Id, ChildRecordId or ParentContentFolderId using the equals operator
2017-10-10 04:55:01,087 ERROR [ContentFolderMember] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction: ContentFolderMember requires a filter by a single Id, ChildRecordId or ParentContentFolderId using the equals operator
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction: ContentDocumentLink requires a filter by a single Id on ContentDocumentId or LinkedEntityId using the equals operator or multiple Id's using the IN operator.
2017-10-10 04:55:22,674 ERROR [ContentDocumentLink] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction: ContentDocumentLink requires a filter by a single Id on ContentDocumentId or LinkedEntityId using the equals operator or multiple Id's using the IN operator.
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction: When querying the Vote object, you must filter using the following syntax: ParentId = [single ID], Parent.Type = [single Type], Id = [single ID], or Id IN [list of ID's].
2017-10-10 04:58:51,926 ERROR [Vote] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: Implementation restriction: When querying the Vote object, you must filter using the following syntax: ParentId = [single ID], Parent.Type = [single Type], Id = [single ID], or Id IN [list of ID's].
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: ContentHubRepositoryId,ExternalId or Id must be specified in your query
2017-10-10 04:58:54,720 ERROR [ContentHubItem] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: ContentHubRepositoryId,ExternalId or Id must be specified in your query
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: FieldDefinition: 列を絞り込む場合、条件は必須です [EntityDefinitionId,DurableId]
2017-10-10 05:01:43,717 ERROR [FieldDefinition] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: MALFORMED_QUERY: FieldDefinition: 列を絞り込む場合、条件は必須です [EntityDefinitionId,DurableId]


```

Fix Example subquery:
```
SELECT Id, QualifiedApiName, (SELECT DurableId, SortOrder FROM CompactLayoutItems) FROM FieldDefinition WHERE EntityDefinition.QualifiedApiName = 'Account' AND QualifiedApiName = 'Name'
```


#  Batch failed: FeatureNotEnabled : Binary field not supported

```
2017-10-10 05:57:51,617 ERROR [ContentVersion] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:76)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
2017-10-10 05:57:51,619 ERROR [ContentVersion] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported


2017-10-10 04:35:31,443 ERROR [Attachment] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:76)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
2017-10-10 04:35:31,444 ERROR [Attachment] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported

....
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
2017-10-10 04:34:27,995 ERROR [ContentVersion] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
2017-10-10 04:35:31,444 ERROR [Attachment] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
2017-10-10 04:41:09,595 ERROR [StaticResource] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
2017-10-10 04:46:38,945 ERROR [Document] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
2017-10-10 04:47:12,871 ERROR [MailmergeTemplate] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported
com.salesforce.dataloader.exception.ExtractException: Batch failed: FeatureNotEnabled : Binary field not supported
2017-10-10 04:58:28,414 ERROR [Scontrol] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: FeatureNotEnabled : Binary field not supported

```

Dataloader is not support for  base64,xsd:base64Binary


#  Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: WHERE 句には JobType 項目式を設定する必要があります。

- FlexQueueItem
- ListViewChartInstance
- DataStatistics
- PlatformAction

```
2017-10-10 04:35:23,015 ERROR [FlexQueueItem] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: WHERE 句には JobType 項目式を設定する必要があります。
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:76)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
2017-10-10 04:35:23,016 ERROR [FlexQueueItem] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: WHERE 句には JobType 項目式を設定する必要があります。

....
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: WHERE 句には JobType 項目式を設定する必要があります。
2017-10-10 04:35:23,016 ERROR [FlexQueueItem] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: WHERE 句には JobType 項目式を設定する必要があります。
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: Getting all ListViewChartInstances is unsupported
2017-10-10 04:41:59,994 ERROR [ListViewChartInstance] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: Getting all ListViewChartInstances is unsupported
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: Where clauses should contain StatType
2017-10-10 04:48:51,878 ERROR [DataStatistics] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: Where clauses should contain StatType
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: すべての PlatformAction エンティティの取得はサポートされていません。
2017-10-10 04:56:42,735 ERROR [PlatformAction] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: EXTERNAL_OBJECT_UNSUPPORTED_EXCEPTION: すべての PlatformAction エンティティの取得はサポートされていません。

```


# Failed to process query: UNKNOWN_EXCEPTION: An unexpected error occurred. Please include this ErrorId if you contact support

```
2017-10-10 07:15:40,343 ERROR [DatacloudAddress] action.AbstractAction handleException (AbstractAction.java:222) - Exception occured during loading
com.salesforce.dataloader.exception.ExtractException: Batch failed: InvalidBatch : Failed to process query: UNKNOWN_EXCEPTION: An unexpected error occurred. Please include this ErrorId if you contact support: XXXXXX-XXX (-XXXXXXXXX)
	at com.salesforce.dataloader.action.visitor.BulkQueryVisitor.executeQuery(BulkQueryVisitor.java:76)
	at com.salesforce.dataloader.action.visitor.AbstractQueryVisitor.visit(AbstractQueryVisitor.java:77)
	at com.salesforce.dataloader.action.AbstractExtractAction.visit(AbstractExtractAction.java:57)
	at com.salesforce.dataloader.action.AbstractAction.execute(AbstractAction.java:131)
	at com.salesforce.dataloader.controller.Controller.executeAction(Controller.java:121)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:149)
	at com.salesforce.dataloader.process.ProcessRunner.run(ProcessRunner.java:100)
	at com.salesforce.dataloader.process.ProcessRunner.main(ProcessRunner.java:253)
2017-10-10 07:15:40,344 ERROR [DatacloudAddress] progress.NihilistProgressAdapter doneError (NihilistProgressAdapter.java:58) - Batch failed: InvalidBatch : Failed to process query: UNKNOWN_EXCEPTION: An unexpected error occurred. Please include this ErrorId if you contact support: XXXXXX-XXX (-XXXXXXXXX)
```