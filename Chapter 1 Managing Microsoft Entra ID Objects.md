# Microsoft Entra ID: An Overview

**Microsoft Entra ID**, previously named **Azure Active Directory (AAD)**, is a **cloud-based Identity and Access Management (IAM)** service provided by Microsoft and is an integral part of the Azure cloud platform. It allows organizations to manage user accounts and control access to resources, both on-premises and in the cloud. Microsoft Entra ID provides a centralized location for managing user **authentication** and **authorization** across multiple applications, platforms, and devices.

Microsoft Entra ID is designed to integrate with other Microsoft services such as **Office 365, Azure, and Dynamics 365**, as well as with third-party cloud services and applications. It provides a variety of features for IAM, such as:

* User and group management
* Application management
* Device management
* Identity protection
* **Single Sign-On (SSO)**
* **Multi-Factor Authentication (MFA)**

Microsoft Entra ID also provides security and compliance features such as **Conditional Access** policies, identity protection, threat intelligence, and auditing and reporting capabilities. This makes it a crucial component of many organization’s **security and compliance strategies**.

In Microsoft Entra, a **user** is an identity that is used to authenticate and authorize access to resources in an organization’s environment.

<img width="1650" height="398" alt="image" src="https://github.com/user-attachments/assets/0340824c-28b3-4bf5-832c-25eb5ab7ef22" />

---

## Microsoft Entra Groups

**Microsoft Entra groups** are a powerful feature within Microsoft’s cloud-based IAM service. These groups allow organizations to organize users, devices, and resources into logical units to simplify and streamline access management.

The benefits of Microsoft Entra groups include the following:

* **Centralized Management**: Easily manage access to resources and permissions for multiple users in one place, reducing administrative overhead.
* **Role-Based Access Control (RBAC)**: Assign roles and permissions to groups instead of individual users, enabling efficient and secure access management.
* **Dynamic Group Membership**: Automatically update group membership based on user attributes, ensuring the right users have access to the resources they need.
* **Collaboration**: Enhance collaboration by granting access to shared resources, such as Microsoft 365 groups, SharePoint sites, and Teams.
* **Reduced Security Risks**: Minimize the risk of unauthorized access by regularly reviewing and managing group memberships.

### Group Types

There are two main group types:

1.  **Security Groups**: These groups serve the same function as traditional on-premises groups, which is to **secure objects** within a directory (in this case, objects within Microsoft Entra).
2.  **Microsoft 365 Groups**: These groups are used to provide a group of people access to a **collection of shared resources** that is not limited to Microsoft Entra ID but also includes shared mailboxes, calendars, SharePoint libraries, and other Microsoft 365-related services.

Security groups are used as container units to group users or devices together. There are three main **membership types** for security groups:

* **Assigned**: Where you manually assign users to a group.
* **Dynamic User**: Where you can specify parameters to automatically group users (e.g., grouping all users who have the same job title).
* **Dynamic Device**: Where you can specify parameters to automatically group devices (e.g., grouping all devices that have the same operating system version).

---

## Administrative Units (AUs)

**Microsoft Entra AUs** are a feature that allows organizations to group users and resources in **logical containers**, based on administrative or geographic boundaries. AUs enable you to **delegate administrative control** over specific subsets of users and resources to different administrators, based on role or location.

For example, a global organization can use AUs to delegate control of users and resources to administrators, based on regions or departments. This helps ensure that each AU has control over only the resources it needs, without interfering with other units. AUs provide a simple and effective way to manage the complexity of large organizations and help organizations maintain control over their resources, while reducing administrative overhead.

The following roles can be assigned within an AU:

* Authentication administrator
* Groups administrator
* Help desk administrator
* License administrator
* Password administrator
* User administrator

<img width="1386" height="623" alt="image" src="https://github.com/user-attachments/assets/15b9c7ba-4794-42a4-9bb1-654b525154b2" />

---

## Core Microsoft Entra Components

The following list outlines these components and how they work together to support Microsoft Entra ID features:

* **Identity**: An Azure identity represents an individual or entity that can interact with Azure resources. It is used for **authentication, authorization, administration, and auditing** purposes, ensuring secure access to resources within an Azure environment. Azure identities can be associated with users, applications, or services.
* **Account**: An account in the context of Microsoft Entra typically refers to a **user account**. A user account is an individual identity associated with a person within an organization or an external partner. Each account contains a unique username and is authenticated against the tenant’s directory.
* **Microsoft Entra ID Account**: An Entra ID account is a specific type of user account that represents a user’s identity across various applications and services. Entra ID accounts enable users to access both internal and external resources with **Single Sign-On (SSO)** capabilities.
* **Microsoft Entra Tenant**: A Microsoft Entra tenant represents a **single organization’s instance of Microsoft Entra ID**, containing all relevant data, such as users, groups, devices, and application registrations. This tenant serves as both an **administrative and security boundary**. It is identified by a unique ID and a domain name (e.g., *example.onmicrosoft.com*).
* **Microsoft Entra Directory**: While the terms *directory* and *tenant* are often used interchangeably, the directory is essentially a **logical container within a tenant**. It organizes and stores resources and objects related to IAM, including users, groups, applications, devices, and other directory objects. **A Microsoft Entra tenant comprises a single directory.**
* **Azure Subscription**: An Azure subscription is a logical entity used to **provision and manage Azure resources**. It is associated with an Azure account and provides access to Azure services, based on a specific pricing tier. Subscriptions help organizations manage costs, monitor usage, and organize resources.

---

## Comparison to Active Directory Domain Services (AD DS)

**AD DS** is a Windows Server-based service that provides centralized authentication and authorization for Windows-based computers. It is designed for on-premises networked resources.

Here are some feature comparisons between AD DS and Microsoft Entra ID:

| Feature | AD DS (On-Premises) | Microsoft Entra ID (Cloud-Based) |
| :--- | :--- | :--- |
| **Primary Role** | Primarily a **directory service** designed for on-premises environments. | A full **IAM solution** optimized for internet-based applications; can also manage on-premises resources. |
| **Protocols** | Uses the **Kerberos** protocol for authentication. | Supports multiple protocols, including **SAML, OAuth, and OpenID Connect**, relying largely on HTTP/HTTPS. |
| **Federation** | **Does not support** federation with other identity providers. | **Supports federation** with other identity providers. |
| **Structure** | Has a **hierarchical structure** (domains, trees, forests, OUs, Group Policy). | Has a **flat structure** organized around tenants. |
| **Managed Services** | You are responsible for managing the infrastructure and servers. | **Microsoft manages the infrastructure**; you manage user accounts, groups, and access policies. |

---

## External Identity Management

### Business-to-Consumer (B2C)

**Azure Active Directory B2C (Azure AD B2C)** is a cloud-based IAM service specifically designed to handle **customer-facing applications**. It allows organizations to provide their customers with secure access to applications and resources. It enables organizations to securely manage user identities, authenticate users, and provide SSO capabilities for their applications, websites, and mobile apps.

### Business-to-Business (B2B)

**Microsoft Entra B2B collaboration** is a feature within Microsoft Entra External ID that allows organizations to invite **external users** to collaborate securely. This feature enables external users to access an organization’s applications and services without compromising the security of its data. Microsoft Entra provides a range of controls for managing B2B collaboration, including customized invitations, self-service sign-up, and access monitoring.

---

## Management Blades

### User Account Management

To manage a user account, you navigate to the **Users** menu in Microsoft Entra ID and select the user. The management screen is the **User management blade**, which contains the following settings:

* **Overview**: View and modify user details, such as name, job information, and user type.
* **Assigned roles**: Displays all role assignments (eligible, active, or expired).
* **Administrative units**: Shows the AUs of which a user is a member.
* **Groups**: Displays the Entra ID groups that a user is part of.
* **Applications**: Shows the applications assigned to a user.
* **Licenses**: Displays what licenses are currently assigned to a user account.
* **Devices**: Shows the devices associated with a user account (e.g., Microsoft Entra-joined).
* **Azure role assignments**: Displays the resources on a subscription level to which an account has access.
* **Authentication methods**: Displays a user’s authentication contact information (phone number, email for MFA). You can also set the account to re-register for MFA or revoke current MFA sessions.

### Group Settings Management

The **Group settings management pane** is accessed by navigating to the **Groups** menu and selecting a group. The options under this blade are as follows:

* **Overview**: Displays general group information (membership type, source directory, object ID, creation date).
* **Properties**: Contains general settings (group name, description, group type, membership type).
* **Members**: Displays all current members. You can also perform bulk operations here.
* **Owners**: Displays the owners of a group who can modify it and its members.
* **Administrative units**: Displays the AUs that a group is part of.
* **Group memberships**: Displays all the security groups that this group belongs to (nested grouping).
* **Applications**: Displays the application assignments.
* **Licenses**: Displays the licenses assigned to a group, which members inherit automatically.
* **Azure role assignments**: Displays the resources on a subscription level to which the group members have access.
* **Dynamic membership rules**: Displays the configuration rules for dynamic groups, allowing you to change the criteria that affect group members.

  <img width="1650" height="1019" alt="image" src="https://github.com/user-attachments/assets/c10bab27-fe0a-4595-a6cb-33bbdcfba7fb" />


