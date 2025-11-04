Chapter 6 Understanding Storage Accounts

In this chapter, you are going to learn about the following main topics:

Understanding Azure Storage Accounts
Creating and Configuring Storage Accounts

<img width="1580" height="1276" alt="image" src="https://github.com/user-attachments/assets/72af7cea-bc63-4934-8984-74042f6e5062" />


Understanding Azure Storage Accounts
Azure offers a variety of services that can be utilized for storage; these can vary from database options to messaging systems to files. One of these services for supporting your storage needs is Azure storage accounts. Azure has created four core types of services as part of Azure storage accounts: Blob Storage, Azure Files, Queue Storage, and Tables Storage. All these services can be consumed from a Standard general-purpose v2 (Standard GPv2) storage account, and some can be consumed individually as the Premium variations (such as Azure Files and Blob Storage), where more performance is required. Various types of data—such as files, documents, datasets, blobs, and virtual hard disks (VHDs)—can be stored in the storage account, and most will be accommodated by the defined structure. The following figure illustrates the different storage services associated with a storage account.

Before creating your storage account, it is important to consider the level of performance required for your storage. Azure distinguishes between two performance grades of service by associating the performance categories directly with different grades of hardware that back the offerings. It is important to note that you cannot convert the type you have selected, and if you later discover that it does not meet your requirements, you will then need to redeploy your storage to the preferred grade of performance tier.

Standard
The Standard storage performance tier is backed by spinning magnetic hard disk drive (HDD) infrastructure, which is the lowest performance grade of hardware storage available through Azure. The benefit of consuming this storage grade is affordability, as you pay a lower price per GB. It is most suitable for storage requirements where you experience low-frequency usage scenarios or large data stores where performance is not as much a concern as the capacity requirement, and you have constrained budgets.

Premium
The Premium storage performance tier offers superior performance to the Standard option, as it is backed by solid-state drive (SSD) storage infrastructure. You will benefit from low latency and fast throughput by selecting this tier of storage for your storage account. It is most suitable for applications requiring extensive disk I/O operations, such as databases. Premium storage costs more than the Standard tier and is directly proportionate to the performance you require.

As you can see, understanding your storage performance requirements is fundamental to deciding on the type of storage you will deploy to meet your storage needs.

Azure Storage currently offers several different types of storage accounts, as detailed in this section. There are various components to consider when choosing the correct type of account, including the following:

Type of storage account (consider the service required)
Redundancy
Intended usage
Performance
Replication
Security
Limitations

The Standard GPv2 storage account is a Standard performance tier account. It supports several services as part of its construct: blobs, queues, tables, and file shares. This is the storage account type recommended for most scenarios due to its versatility in storage services and is the default option. It also supports several storage redundancy options: locally redundant storage (LRS), geo-redundant storage (GRS), read-access geo-redundant storage (RA-GRS), zone-redundant storage (ZRS), geo-zone-redundant storage (GZRS), and read-access geo-zone-redundant storage (RA-GZRS). The following figure illustrates the set of services offered by the storage account:

<img width="1276" height="524" alt="image" src="https://github.com/user-attachments/assets/08b06555-3c58-4599-8e0a-96c62e1cbb43" />

Blob Storage
The storage solution created to cater to object storage in Azure is Azure Blob Storage. Blob Storage offers unstructured data storage in the cloud and can store all kinds of data, such as documents, VHDs, images, and audio files. Azure Blob Storage is Microsoft's object storage solution for the cloud. Blob Storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.
There are three types of blobs that you can create:

Page blobs: Blobs that are used for the storage of disks. These blobs are optimized for read and write operations and stored in 512-byte pages. If you have a VHD that needs to be stored and attached to your VM, you will create a page blob. The maximum size of a page blob is 8 tebibytes (TiB).
Block blobs: Basically, these cover all the other types of data that you can store in Azure, such as files and documents. The maximum size of a block is 4,000 mebibytes (MiB) and the maximum size of a blob is 190.7 TiB.
Append blobs: These blobs are optimized for append operations, basically meaning that data (blocks) is added to the end of a blob. Each block can be of different sizes, up to a maximum of 50,000 blocks. Updating or deleting existing blocks written to the blob is unsupported. Use cases include logging and auditing.
The Blob Storage offering within the Standard GPv2 storage account supports all the preceding blob types. Where more performance is required, consider using the Premium blob offerings.

In addition to the variety of storage services, the Standard GPv2 storage account offers multiple access tiers that consist of hot, cool, cold, and archive storage. These storage tiers will be covered later in this chapter, in the Storage Access Tiers section.

Example use cases for Blob Storage include the following:

Backup and archiving data
Disaster recovery (DR) datasets
Streaming media content (such as audio and video)
Storing unstructured data

Blob Storage is designed for:

Serving images or documents directly to a browser.
Storing files for distributed access.
Streaming video and audio.
Writing to log files.
Storing data for backup and restore, disaster recovery, and archiving.
Storing data for analysis by an on-premises or Azure-hosted service.

Blob Storage offers three types of resources:

The storage account
A container in the storage account
A blob in a container
The following diagram shows the relationship between these resources.

<img width="331" height="111" alt="image" src="https://github.com/user-attachments/assets/1ed7fce0-ab43-4aa2-b7de-9b2d2c6e8625" />

Queue Storage
Azure Queue Storage is a service designed for storing messages in Azure. Messages are used to enable decoupled infrastructure to be able to communicate by sending data for processing. This data is typically consumed in an asynchronous format by the services reading the queue that the messages are stored in. Each queue can be thought of as a line where messages are placed waiting to be processed, with each queue normally relating to a particular topic of message for your services. For instance, imagine you run a website that receives photos, and you frame them on canvases.

You could have two queues for your application, one indicating that a new image has been uploaded to your site and needs to be processed, and another one for purchases that have been made and scheduling an order. The respective components of your application would process these queues independently of each other and systematically through received messages in each respective queue. By decoupling the various components of your application, you can create highly resilient and scalable infrastructure as each layer of the application can be managed independently of each other. When a problem occurs, only the affected part of the application stops working. When you need to scale, you can scale at a granular level (for those components that require scale only).

Table Storage
Azure Table Storage is a solution designed for the storage of NoSQL data (non-relational structure data). Data is stored in tables, hence the name Table Storage. By design, Table Storage is schemaless and therefore adapted to easy consumption of data into the database as you do not have to specify the data structure before being able to ingest it. It is flexible in structure and can evolve with your application, meeting its changing demands. Table Storage is a cost-effective solution for many basic database needs, such as storing the user data required by your applications.

Azure Files
With Azure Files, you can create file shares in the cloud. Using the version of Azure Files available to the Standard GPv2 storage account, you can access your files using the Server Message Block (SMB) protocol, which is an industry standard that can be used on Linux, Windows, and macOS devices. Azure Files can also be mounted as if they were a local drive on these same devices, and they can be cached for fast access on Windows Server using Azure File Sync. File shares can be used across multiple machines, which makes them suitable for storing files or data that are accessed from multiple machines, such as tools for development machines, configuration files, or log data. Azure Files is part of the Azure Storage client libraries and offers an Azure Storage Representational State Transfer Application Programming Interface (REST API) that can be leveraged by developers in their solutions.

Premium Block Blobs
Premium storage is used for situations requiring low latency and high performance. Premium storage performance is enabled through the underlying high-performance hardware associated with the presentation of storage within Azure, such as through SSDs, and provides faster throughput and input/output operations per second (IOPS) compared to Standard storage, which is backed by hard disks (spinning disks). This storage is typically used for block blobs and append blobs. It supports LRS and ZRS redundancy options.

Premium block blobs leverage Premium Storage to offer high-performance storage for all kinds of files that are stored in block format. Common scenarios where Premium block blobs are used include the following:

Workloads requiring fast access and functionality, such as e-commerce applications
Large datasets that are constantly added, manipulated, and analyzed, such as internet of things (IoT) applications
Artificial intelligence (AI) or machine learning (ML) applications
Data transformation workloads

Premium File Shares
Premium storage is used for situations requiring low latency and high performance. Premium file shares are typically used for workloads requiring enterprise-scale or high-performance applications. The service presents storage in the form of SMB or Network File System (NFS) storage. SMB is typically used for Microsoft Windows environments, such as Windows Server, whereas NFS is typically used for Linux-based environments. NFS can only be enabled on Premium file shares. Some differences worth noting when choosing your file-share storage service are IOPS and provisioned storage limitations. GPv2-backed Standard file shares have a limit of 20,000 IOPS and 5 pebibytes (PiB) of provisioned storage, while Premium file shares storage offers 100,000 IOPS but only 100 TiB of provisioned storage.

Blob storage has a flat-file hierarchy, meaning that it does not work as a filesystem, as we are traditionally used to working with, such as on servers and workstations. While containers may appear as folders, they are only logical structures to emulate a filesystem. Bearing this in mind, Blob Storage is not meant to be consumed directly as a shared storage system, such as SMB or NFS, but through technologies such as BlobFuse, direct storage into a blob can be achieved.

Premium Page Blobs
Premium page blobs are designed for high-performance storage requirements and can offer low-latency access. They are more expensive when compared to Standard storage, which is typically for less demanding storage workloads. This storage is ideal for storing disk-type data for VMs, such as the OS and data disks. It is also recommended for Azure SQL DB persistent storage.

One limitation of Premium page blobs is that they can only use the hot access tier, not the cool or archive tiers. This means that they are not suitable for long-term storage with infrequent access.

Storage Access Tiers
Hot
The hot access tier is most suitable for storing data that is accessed frequently and data that is in active use. For instance, you would store images and style sheets for a website inside the hot access tier. The storage costs for this tier are higher than for the other access tiers, but you pay less to access files. This is the default access tier for storage.

Cool
The cool access tier is the most suitable for storing data that is not accessed frequently (less than once in 30 days). Compared with the hot access tier, the cool tier has lower storage costs, but you pay more to access files. This tier is suitable for storing backups and old content that is not viewed often. The cool tier is ideal for data that will be stored for more than 30 days.

Cold
The cold tier of storage is similar to the cool tier of storage. Again, the cold tier is cheaper than the cool and hot tiers for storage costs but has comparatively higher access costs. The cold tier is ideal for data that will be stored for more than 90 days.

Archive
The archive storage tier is set on the blob level and not on the storage level. It has the lowest costs for storing data and the highest cost for accessing data compared to the hot and cool access tiers. This tier is for data that will remain in the archive for at least 180 days, and it will take several hours of latency before it can be accessed. This tier is most suitable for long-term backups or compliance and archive data. A blob in the archive tier is offline and cannot be read (except for the metadata), copied, overwritten, or modified. Although the blob data remains unreadable in the archive tier, its metadata remains readable. You will need to rehydrate the blob before you can read or alter data within the archive storage. Rehydrating is the process of restoring data from the archive data store to an online storage tier.

The service-level agreement (SLA) for all services when designing and deploying to Azure. The great news with storage accounts is that you are assured of 99% availability of services.

Data tiers can be changed between hot and cool; doing so will charge the full Premium at the conversion of the existing storage tier. This charge does not apply to Blob Storage accounts.

Standard Disk Storage
Standard disk storage offers two flavors: a Standard hard disk drive (HDD) or Standard SSD to store data, and it is the most cost-effective storage tier that you can choose. Standard disk storage can only use LRS or GRS to support high availability (HA) for your data and applications.
The Standard HDD disk type is best suited for scenarios that require infrequent access (such as for backups), dev/test workloads, or workloads with non-critical data. While the Standard SSD disk type is best suited for test and development workloads, most web servers and applications do not require fast throughput or high IOPs.

Premium Disk Storage
With Premium disk storage, your data is stored on SSDs. This storage is faster than the Standard SSD range. Not all Azure VM series can use this type of storage. It can only be used with VM stock-keeping units (SKUS) that contain an S in them, signifying the SSD portion of the VM, such as DS, DSv5, GS, LS, ES, or FS series Azure VMs.

Ultra Disk Storage
Azure Ultra Disks are a type of managed disk designed to provide extremely high performance and low latency for mission-critical and data-intensive workloads. They are suitable for applications that require consistent sub-millisecond latency and high IOPS and throughput.

Managed disks are recommended by Microsoft over unmanaged disks.

Redundancy
Redundancy refers to the number of copies of data that are available at any time; this supports the failure of copies and ensures the continuity of services dependent on the redundancy option chosen. Regardless of the option, data is replicated three times in a storage account for the primary region.

LRS
This is storage that is copied three times synchronously within a single data center in a chosen region. LRS is the cheapest replication option that can be chosen and is not intended for business-critical workloads that require HA or resiliency. Protection is provided against server rack and drive failures; however, the protection is limited against unforeseen disasters that could occur within the data center (such as flooding or fire).


<img width="1511" height="818" alt="image" src="https://github.com/user-attachments/assets/1cafa1ae-8a40-4939-aa56-959bd007eb53" />


ZRS
ZRS maintains three copies of data are copied synchronously across three Azure AZs for the selected region; this protects against failure at a data center layer. Each AZ is a distinct physical site equipped with its own power, cooling, and networking infrastructure. The ZRS redundancy option is recommended for HA within a single region and can provide reliability of at least 99.9999999999% (12 9s) annually. If a zone becomes unavailable, your data is still accessible, both for read and write operations. This option may also be chosen where data residency requirements apply, such as through a compliance standard that the organization aligns with.

<img width="1502" height="630" alt="image" src="https://github.com/user-attachments/assets/241fd001-e398-4279-8dda-a62bc2c34b18" />

GRS
This option is chosen to protect against regional failure while also offering protection within a single data center for each region. Effectively, you get six copies of data (three in each region). Data is copied asynchronously across regions but synchronously within the data center.

<img width="1611" height="714" alt="image" src="https://github.com/user-attachments/assets/2f64f39a-638d-48ff-8324-67c5501276de" />

It is important to note that data copied to the secondary region is inaccessible for read and write operations unless a failover has been initiated. In the failover state, you can choose to select the secondary region as the new primary region, and you will then have the option to read and write data again. To enable read access to data in the secondary region, you should deploy RA-GRS storage.

GZRS
GZRS is chosen to protect against a regional failure while also offering zonal HA and protection within each region. Effectively, you get six copies of data (three in the primary region distributed across AZs, and three distributed within a data center in the secondary region). Data is copied asynchronously across regions but synchronously within the region and data centers. There are two types of GZRS storage, the first being GZRS, where data is replicated but, in the event of a failure, remains inaccessible during the failover process. The second is RA-GZRS, where your data is accessible in the event of a failure in a read-only state in the secondary region during the failover process. You can, however, read and write your data in the new primary region upon completion of the failover for both offerings.

<img width="1311" height="543" alt="image" src="https://github.com/user-attachments/assets/e280bae5-7240-4265-a26b-b5b374fa5ba5" />

The archive tier of storage does not support ZRS, GZRS, and RA-GZRS redundancy options.

Storage Encryption
Encryption is the process of converting data into a format that is unreadable by unauthorized parties, protecting the confidentiality and integrity of the information. This is done using cryptographic algorithms, which require encryption keys to transform the data into an encrypted form (ciphertext) and back to its original form (plaintext). Encryption plays a crucial role in securing sensitive data from unauthorized access, tampering, or theft.

Encrypting data is a vital security measure for safeguarding sensitive information and adhering to various regulations and industry norms. Implementing encryption allows you and your organization to do the following:

Defend confidential data against unauthorized access and potential data breaches
Uphold privacy and foster trust among parties participating in data transactions
Meet the requirements of industry-specific rules and standards (such as GDPR, HIPAA, and PCI DSS) that demand data protection measures
Secure intellectual property, proprietary knowledge, and other valuable data assets
Preserve the integrity of data by deterring tampering and illegitimate modifications
Azure offers the ability to activate encryption at multiple levels within the platform, such as on the infrastructure layer and the storage layer

always advised where possible to maintain the highest levels of security possible.

Storage encryption on Azure: This refers to encryption services provided by Azure to protect data stored within its storage services, such as Azure Blob Storage, Azure Files, and Azure Disks. Azure provides several encryption options, including server-side encryption (SSE) using service-managed keys, customer-managed keys (CMK), or customer-provided keys. Azure Storage uses SSE, which is encryption on the host layer of services within Azure and is used to automatically encrypt data when it is persisted to the cloud. This encryption helps protect your data and meet organizational security and compliance commitments. Azure also supports client-side encryption, where data is encrypted before it is sent to Azure Storage. Some key points to note are as follows:
Azure Storage service-side encryption encrypts data using 256-bit AES encryption, which is FIPS 140-2 compliant.
Encryption is enabled for all storage accounts and cannot be disabled.
Data is encrypted regardless of performance tier, access tier, or deployment model.
There is no additional cost for Azure Storage encryption.
Infrastructure encryption: Infrastructure encryption in Azure storage accounts is an enhanced security feature that offers customers an elevated level of data protection. When this feature is activated, data stored in a storage account undergoes two distinct encryption processes, one at the service level and another at the infrastructure level. This dual encryption approach employs two separate encryption algorithms and keys, ensuring that even in the event of a compromise of one encryption layer, the other layer continues to safeguard the data.
Different Encryption Types on a Storage Account
There are two types of encryption key management available for Azure Storage: Microsoft-managed keys (MMK) and customer-managed keys (CMK):

MMK: By default, data in a new storage account is encrypted with MMK. These keys are managed and maintained by Microsoft, ensuring that the encryption and decryption of data are handled seamlessly without any additional effort from the user. Microsoft also takes care of key rotation, adhering to compliance requirements.
CMK: Users who prefer to have more control over their encryption keys can opt for CMK. With CMK, you can specify your own key for encryption tasks. These keys are stored in the Azure Key Vault or Azure Key Vault Managed Hardware Security Module (HSM) to use for encrypting and decrypting data in Blob Storage and Azure Files. This option allows users to manage and audit key rotation themselves, providing a higher level of control over their data encryption.

SSE: Azure automatically encrypts data before it’s stored in Azure Storage services and decrypts it when accessed. There are three key management options for SSE:
Service-managed keys: Azure automatically manages the encryption keys. This is the default option, and it requires no additional configuration.
CMK: Customers can manage their encryption keys using Azure Key Vault. This provides greater control over key management and rotation.
Customer-provided keys: Customers can supply their encryption keys for each data transaction. This offers the highest level of control but also requires more management overhead.
Client-side encryption: Data is encrypted by the client application before it’s sent to Azure Storage. Decryption also occurs on the client side when the data is accessed. This approach ensures that data is encrypted both in transit and at rest in Azure Storage, and it gives customers full control over the encryption process and key management.

Storage accounts: https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview

Azure Blob Storage: https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction

Blob access tiers: https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview

Understanding block blobs, append blobs, and page blobs: https://learn.microsoft.com/en-us/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs

Blobfuse2: https://github.com/Azure/azure-storage-fuse

Rehydrating blob data from the archive tier: https://learn.microsoft.com/en-us/azure/storage/blobs/archive-rehydrate-overview

Storage account SLA: https://azure.microsoft.com/en-us/support/legal/sla/storage

Storage redundancy: https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy








