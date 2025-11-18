Chapter 9 Storage Management and Replication

In this chapter, you are going to cover the following main topics:

Copying Data by using AzCopy
Configuring Storage Replication and Lifecycle Management

Copying Data by Using AzCopy
AzCopy is a utility that can be used for copying files to and from Azure Storage accounts through a command-line-based utility. Authentication for the tool can be conducted using either an Active Directory account or a SAS token from storage. The tool provides many other functions but is primarily designed for file copying. It can also be used for monitoring and managing various other copy jobs. Some of the other features are its delete capability, its sync functionality for replicating storage from one location to another, and even the ability to make containers and file shares. A couple of use cases for AzCopy are replicating data from one storage account to another as a means of backup and migrating from one environment to another (such as development to production). You might also need to process data from the storage account on your local machine or server; AzCopy will enable you to copy files for local processing.

The AzCopy commands are structured in the following format: azcopy [command] [source] [destination] [flags].

Immutable storage (data storage that imposes a restriction whereby once data is written, no alterations or deletions to the data can be made within a predefined period of time) and Permanent delete (whereby you can delete a snapshot or blob version permanently, even before the retention period’s predefined end date) options.

Lifecycle management refers to the management of an object from its creation to its retirement or disposal. These features enable the efficient use of your storage resources through policies that move blob data to different access tiers in accordance with your predefined rules. For example, you can configure a policy to move data not accessed within the last 90 days to cool storage and then transfer it back to the hot tier for enhanced performance when it is required again.

As part of the storage replication and management services section to follow, you will learn about topics such as the Azure File Sync service, blob object replication, blob lifecycle management, blob data protection, blob versioning, immutable storage, and storage account deletion.

The following section will explore the various storage replication services available for Azure Storage.

Azure File Sync
Azure File Sync enables you to synchronize your organization’s file shares (on-premises or similar) with Azure Files, providing a local cache of your data for faster access and improved performance. This allows you to enjoy the flexibility, compatibility, and performance of your local file shares (such as an on-premises file server) but also store a copy of all the data within the file share in Azure.

The service offers versatility when it comes to connectivity, as it allows you to use any protocol that’s available on Windows Server to access your data locally, including Server Message Block (SMB), Network File System (NFS), and File Transfer Protocol over TLS (FTPS).

Blob Object Replication
Blob object replication provides the capability within Azure to replicate blob objects based on replication rules. The copy will run asynchronously between source and destination containers across two different storage accounts. Several rules can be configured for your desired outcome. Note that for replication to be enabled, blob versioning needs to be enabled. Blob object replication is similar to the exercise you completed earlier using AzCopy on the copy side of the replication. The replication for the storage account is conducted automatically once it’s enabled and uses a special technique for detecting changes.

Blob Life Cycle Management
This is a capability available for GPv2 storage accounts, Blob Storage accounts, and Azure Data Lake Storage. It allows the management of the blob lifecycle through rule-based policies. Data can be automatically transitioned to cooler and cheaper tiers using this functionality. Data can also, in accordance with policies, be expired and deleted. The following actions can be applied to blobs based on the requirements, automated data tiering, blob snapshots, blob versioning, and blob deletion. Multiple rules can be created and can also be applied to a subset of blobs and containers through filters such as name prefixes. If multiple rules are created, you will need to apply the rules in order of tier temperature, moving from hot to cool, then from cool to cold, then to archive, and then to deletion. Pricing for blob lifecycle management is based upon tier operational charges, but the service itself is free, and delete operations are also free. It should be noted that this is a great feature to assist in the optimization of your overall storage account costs by automatically transitioning between tiers.

Blob Data Protection
Blob data protection is a mechanism that assists with the recovery of data in the event of data being deleted or overwritten. The implementation of data protection is a proactive measure to secure data before an incident occurs. Azure Storage provides the capability of protecting data from being deleted or modified, as well as the restoration of data that has been deleted or modified. Soft delete for containers or blobs enables you to restore data based on a chosen period for retaining deleted data; the default configuration is seven days. When you restore a container, the blobs, as well as the versions and snapshots, are restored.

Blob Versioning
Blob versioning enables a blob to maintain several versions of an object, which can be used for restoring blob data as the version captures the current state of the blob upon being created or modified. This operation is run automatically when blob versioning is enabled. Blob versioning is a powerful feature as it enables you to restore data if it has been modified or deleted. There are several use cases where this may be useful to you:

Data recovery: Restore data to a previous version if it has been deleted or modified. This is particularly useful for the restoration of accidentally deleted data.
Compliance: With blob versioning, a history of all changes is maintained, which is crucial for audit trails and meeting any compliance requirements you may need to adhere to, such as a rule where data cannot be deleted for seven years. You can also see who made changes and when.
Application development: While developing applications, many changes can happen to code files. A version history will allow the recovery of any data that it stores.
Data anaylsis: Historical data can be beneficial for data analysts looking to analyze trends and make comparisons of metrics over time.
Backup and restore: Blob versioning can act as an additional layer of backup and remove the need for solely relying on traditional backup solutions.

Immutable Storage
Immutable storage, often referred to as Write Once, Read Many (WORM), can be configured on Blob Storage. This is often used to protect data from accidental deletion or overwrites. Often, there is a legal requirement to manage data in this manner. It is always advised that you understand your organization’s governance requirements regarding data to ensure you comply with them.

Immutable storage can be configured with two types of policies:

Time-based retention policies: Data objects are managed against a time policy for the duration that the active policy data follows WORM, but after the expiration of this, data may be deleted but not overwritten.
Legal hold policies: Data is held in a WORM state until the legal hold policy is explicitly cleared. This is often for litigation requirements.

Container soft delete can only restore the entire container with all the contents, not individual blobs. To achieve blob-level recovery capability, soft delete for blobs should be enabled.

Storage Account Deletion
There are circumstances when you may delete a storage account and, after deletion, realize that you need to recover the data. In these instances, the storage account can potentially be recovered, provided the account was deleted fewer than 14 days ago and the following requirements are also met:

The storage account was created using the ARM model
A storage account with the same name has not been provisioned since the deletion of the storage account in question
The user performing the recovery has the appropriate permissions

Working with Azure File Snapshots
File snapshots are point-in-time, read-only copies of data as found in Azure file shares. These snapshots enable you to restore previous versions of files, protecting against data corruption and unwanted changes or deletions and providing backup functionality. A couple of examples of where this might be useful are recovering data from accidental deletions and reverting to previous versions of a file (such as a development version) if previous iterations of a file are needed.

You are encouraged to read up further on the topic by using the following links:

Azure File Sync: https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-introduction

Configuring object replication: https://learn.microsoft.com/en-gb/azure/storage/blobs/object-replication-configure

Blob versioning: https://learn.microsoft.com/en-gb/azure/storage/blobs/versioning-overview

Blob lifecycle management: https://learn.microsoft.com/en-us/azure/storage/blobs/lifecycle-management-overview

Blob data protection overview: https://learn.microsoft.com/en-us/azure/storage/blobs/data-protection-overview
