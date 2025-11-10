Chapter 7 Copying Data To and From Azure

Using Azure Data Box (previously, Import/Export)
Installing and Using Azure Storage Explorer
Configuring Azure Files and Azure Blob Storage

Azure Data Box (previously known as Azure Import/Export) is a service that allows you to import and export data quickly and securely to and from an Azure data center. Imported data is stored either in Azure Blob Storage or Azure Files. The value of the Azure Data Box service is overcoming the limitations experienced in network capacity, time, or costs when transferring data into or out of Azure. By utilizing Azure Data Box, you can transfer large amounts of data quickly into or out of Azure affordably.

To use Azure Data Box, you will need to prepare disk drives that will be shipped to the Azure data center. These disk drives must have BitLocker encryption enabled. Once the volume is encrypted, you can copy your data to the drives before shipment. After encryption, a disk needs to be prepared using the WAImportExport.exe tool. By running this tool, a journal file is automatically created in the same folder that you ran the tool. There are two other files created as well – a .xml file and a drive-manifest.xml file. 

Importing into an Azure Job

<img width="1555" height="1119" alt="image" src="https://github.com/user-attachments/assets/2b46f74f-466f-4ed6-9ba3-d7c8f3ead074" />

Exporting from an Azure Job

<img width="1572" height="1094" alt="image" src="https://github.com/user-attachments/assets/e44a420d-2493-4ffe-9753-98f9d59c8399" />

Installing and Using Azure Storage Explorer
Azure Storage Explorer is a standalone application that can be used to easily work with the different types of data stored in an Azure storage account. There is also an implementation in preview in the Azure portal that allows integrated access to storage accounts. You can upload, download, and manage files, queues, tables, blobs, data lake storage, and Cosmos DB entities using Azure Storage Explorer. Aside from that, you can also use the application to configure and manage cross-origin resource sharing (CORS) rules for your storage accounts. This application can be used on Windows, Linux, and macOS devices.

Another method to navigate files is to use the breadcrumb navigation at the top of the screen. You can navigate back to the respective sections by clicking them; in this example, clicking az104storageaccountdemo1 | File shares will take you back.

Storage Explorer simplifies the process of working with Azure storage without requiring you to install or configure additional tools to work with it. With Storage Explorer, you have consistent user experience across devices, even on different operating systems.

In this exercise, you have learned the following skills pertaining to Azure Files – creating a file share, mapping a file share, uploading and downloading data from a file share, and deleting a file share. Working with file shares is a simple way to share data among several servers and services using the SMB protocol. File shares are organized into a hierarchical structure, similar to most desktop systems, allowing easy navigation and categorization. This makes working with file shares seamless when transitioning from traditional storage mechanisms, such as disks on VMs.

blob storage has no filesystem, it maintains a flat structure.

As mentioned earlier in the chapter, there are four storage tiers available for Azure Blob Storage – namely, hot, cool, cold, and archive, which can only be set for blob storage. The storage tier can be configured both during the creation of a storage account – where settings apply to the entire account by default (these will be reflected as inferred) – and at the blob level. Changing blob storage tiers allows more granular control of the performance and reliability characteristics required of each blob, such as in backup-type solutions or for Disaster Recovery (DR) scenarios. It is possible to change between tiers at any stage; however, bear in mind that tier changes result in pricing considerations, as the operations incur charges in the changing of tiers. For example, changes from hot to cool or archive, and from cool to archive, will incur write charges (operation and access charges). For changes from archive to cool, cold, or hot, and from cool to hot, read charges will be incurred (operation and access charges).

Azure URL Paths for Storage
The storage services each contain their own endpoint links, relative to the service they provide (such as file or blob), which are labeled as part of the Fully-qualified Domain Name (FQDN) and begin with the storage account name. You are expected to know the construction of all storage endpoints for the exam. Having this knowledge will also assist you in more easily constructing endpoint FQDNs to connect to your services. These service endpoints can be used through Storage Explorer or programmatically (such as scripts).

The following is a summary of each endpoint by service type:

Azure Files: https://[storageAccountName].file.core.windows.net
Blob Storage: https://[storageAccountName].blob.core.windows.net
Queue Storage: https://[storageAccountName].queue.core.windows.net
Table Storage: https://[storageAccountName].table.core.windows.net
Data Lake Storage: https://[storageAccountName].dfs.core.windows.net
Static website: https://[storageAccountName].[zone].web.core.windows.net
These can also be found on the Endpoints menu when browsing the storage account on the portal. There is another set of endpoints that you should be aware of when making use of Azure DNS zone endpoints on the storage account, which are as follows:

Azure Files: https://[storageAccountName].z[00-50].file.storage.azure.net
Blob Storage: https://[storageAccountName].z[00-50].blob.storage.azure.net
Queue Storage: https://[storageAccountName].z[00-50].queue.storage.azure.net
Table Storage: https://[storageAccountName].z[00-50].table.storage.azure.net
Data Lake Storage: https://[storageAccountName].z[00-50].dfs.storage.azure.net
Static website: https://[storageAccountName].z[00-50].web.storage.azure.net
Note the addition of z[00-50] in each endpoint, compared to the standard endpoints; this denotes a zone that is automatically selected between 0 and 50 as a double-digit representation, which is why you see 00.

Note

At the time of writing, this function is still under preview. It should also be noted that Azure DNS Zone endpoints are only supported for the Azure Resource Manager (ARM) deployment model.
