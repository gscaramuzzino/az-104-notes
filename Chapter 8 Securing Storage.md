Chapter 8 Securing Storage

Configuring Network Access to Storage Accounts
Storage Access Keys
Working with SAS tokens
Configuring Access and Authentication

Configuring Network Access to Storage Accounts
One of the first security concepts you should consider when securing your storage account is to consider how and where your storage account is accessed. You can secure your storage account to a specific set of supported networks, which are granted access by configuring network rules so that only applications that request data over the specific set of networks can access the storage account. When these network rules are effective, the application needs to use proper authorization on the request. This authorization could be through either Entra ID credentials for blobs and queues, a SAS token, or a valid account access key.

Public Endpoints
By default, storage accounts are provisioned with a public endpoint, and thanks to the enhanced control Azure offers, network traffic can be limited to those trusted IP addresses and networks to which you have granted access on Azure. For good security practice, all public access to storage accounts should be set to deny for the public endpoint by default, unless public access is specifically required. The network rules defined for the storage account will apply across all protocols, including Server Message Block (SMB) and Representational State Transfer (REST). Therefore, to allow access, an explicit rule will need to be defined. There are additional exceptions that can be configured that give you the ability to allow access to Azure services on the trusted services list to the storage account, as well as configuring logging and metric access for any networks (such as for Log Analytics).

Azure Virtual Network (VNet) Integration
There are occasions where you require your traffic to still flow securely from your application whilst allowing certain inbound traffic from over the internet. You may want to explicitly allow only certain VNets within your Azure environment to access this storage account. 

 Enabled from selected virtual networks and IP addresses.

 You have now completed this section on network restrictions on public endpoints. Should you wish to test connectivity with this, you can deploy a virtual machine (VM) in the same VNet as the storage account and connect to the storage account from inside the VM. In the next section, you will learn about private endpoints.

Private Endpoints
Private endpoints provide a mechanism for Azure Storage accounts to have a private interface for a storage account and can be used to eliminate public access. They provide enhanced security over a public endpoint because they prevent unauthorized access by not being exposed publicly. When implementing a private endpoint, a network interface card (NIC) is associated with the storage account and will be placed in a VNet. The traffic for the storage account will traverse the VNet with which it is associated. Private endpoints are provided through a service called Private Link.

Network Routing from Storage Accounts
The default network routing preference option chosen for storage accounts and most Azure services will be for the Microsoft network. This is a high-performance, low-latency global connection to all services within Azure and serves as the fastest delivery service to any consumer service or user. This is due to Microsoft configuring several points of presence within their global network. The closest endpoint to a client is always chosen. This option costs slightly more than traversing the internet. If you select Internet routing, then traffic will be routed in and out of the storage account outside the Microsoft network.

Configure Azure Storage firewalls and virtual networks: https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security

Use private endpoints for Azure Storage: https://learn.microsoft.com/en-us/azure/storage/common/storage-private-endpoints

Private Link resources: https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-overview

Storage Access Keys
Storage access keys are like passwords for your storage account and Azure generates two of these when you provision your account, namely a primary and secondary key. Just like passwords, they need to be changed from time to time to ensure you are not compromised through potential leakage (such as in code files). Whilst this scenario may feel uncommon, it is a very real risk, and for this reason, it is best to change your keys every few months. This practice is referred to as key rotation.

As a recommendation, key2 should be rotated first and updated for any relevant applications and services, then followed by key1. This process ensures that the primary key (key1) is not directly impacting all business-critical services and causing unnecessary downtime. The rotation process should still be properly planned and maintained through an appropriate change control process within your organization.

Note

As a best practice, keys should be rotated every 90 days to prevent unauthorized exposure to the account. This will also limit the potential attack window for compromised SAS tokens.

Working with SAS Tokens
SAS tokens are secure access tokens that provide delegated access to resources on your storage account. The storage service confirms the SAS token is valid in order to grant access. The construct of a SAS token includes the permissions granted on the token, the date validity, and the signing key for the storage account. When creating a SAS token, several items that govern the process of granting access at a granular level need to be considered. They are as follows:

Resource types that the client might use
Permissions on the resource types that are required
The period the SAS key should function for
Types of SAS
There are three types of SAS supported by Azure Storage:

User-delegated SAS: This is a SAS token that is secured by Entra ID credentials.
Account SAS: An account SAS is created and secured using a storage key. The permissions granted can span several services (blob, file, queue, and table), as well as accessing permissions for the chosen services.
Service SAS: A service SAS is identical to an account SAS except that it is limited to a single service. There are limitations to some read, write, and delete operations for a service SAS that the account SAS has higher privileges to allow.
Forms of SAS
SAS tokens can take two forms, as detailed here:

Ad hoc SAS: This SAS token is created as needed where permissions are chosen along with accessible services in alignment with the type of SAS used. The configuration is specified in the SAS URI. This is generally used for scenarios where quick access is required for a temporary period. SAS tokens cannot be managed after being issued. User-delegated SAS and account SAS can only be provisioned as an ad hoc SAS.
Service SAS with stored access policy: This form of SAS token is more secure and enhances the functionality upon that which an ad hoc SAS token delivers. Service SAS tokens can be managed after being issued and are manufactured to comply with policies configured in the stored access policy. SAS tokens can be modified and deleted using a stored access policy.

Blob versioning permissions allows you to have multiple copies of files if you need to restore against any changes made. This may be something that causes risk by allowing users to delete versions. 

Allowed protocols should be limited to HTTPS on the SAS creation for enhanced security. The SAS start and end time should be limited as far as possible to the necessary time required for access.

Stored Access Policies
A stored access policy provides an additional layer of control over SAS by introducing policies for managing the SAS token. SAS tokens can now be configured for a start and expiry time with the ability to edit and revoke access after they have been issued. This added functionality can prove to be tremendously useful when it comes to managing access to your storage accounts in the future using SAS-based access. Without access policies, your provisioned SAS access will be available for the defined period you had at issue time unless you change the signing keys for the storage account.

In this section, you learned about SAS tokens, the different types you get (user delegation SAS, service SAS, and account SAS), the forms they can be consumed in (ad hoc SAS and service SAS with stored access policy), and how to generate them. You also learned about stored access policies and how they provide an additional layer of control over SAS by introducing policies for managing SAS tokens. In the next section, you will learn about the access and authentication features available to storage accounts and configure them on a storage account in an exercise.

Configuring Access and Authentication
In this section, you will explore the various methods of identity-based authentication available to Azure storage accounts. Authentication is the function of verifying an identity, typically through a process of verifying some form of credentials (such as username and password, biometrics, or security tokens). By instituting good authentication practices, you can improve security. Integration into Entra ID or AD is important in leveraging existing and known identities into applications and services as opposed to having unknown users potentially accessing your resources.

Storage accounts provide several identity-based authentication methods as listed in the following list:

AD DS, which is your typical on-premises AD environment
Microsoft Entra Directory Domain Services (Microsoft Entra DS)
Microsoft Entra Kerberos for hybrid identities
AD Kerberos authentication for Linux clients
All the preceding identity-based authentication options offer the ability to utilize Kerberos authentication. Kerberos authentication is a network protocol designed to provide secure authentication, even on unsecured networks, using cryptographic methods. Kerberos relies on tickets in the authentication process.

Domain trusts are relationships established between two or more domains in a network, allowing users in either domain to access resources from each other. 

 There are three primary permissions (authorization) on the SMB share that you should be cognizant of:

Storage File Data SMB Share Reader: This permission grants read access to the SMB share files and directories
Storage File Data SMB Share Contributor: This permission grants read, write, list, and delete access to the SMB share files and directories
Storage File Data SMB Elevated Contributor: This grants contributor access as well as the ability to assign permissions (modify access control lists (ACLs)) to other SMB share files and directories

Also, Network File System (NFS) shares do not support identity-based authentication.
