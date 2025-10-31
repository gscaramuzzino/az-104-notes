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




