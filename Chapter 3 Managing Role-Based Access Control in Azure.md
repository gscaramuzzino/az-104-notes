Chapter 3 Managing Role-Based Access Control in Azure

In this chapter, you will explore the following topics:

- Understanding Azure regions
- Managing Azure subscriptions and management hierarchy
- Configuring management groups
- Understanding RBAC
- Creating a custom RBAC role
- Interpreting access assignments

Understanding Azure Regions
An Azure region is a set of data centers deployed within a specific geographic area. Each region is connected to the Azure backbone network and is designed to be highly available and resilient to ensure maximum uptime for your applications and services. When you create resources in Azure, you have the option to select a specific region where those resources will be located.

The region you choose for your resources can have implications for RBAC management. This is because different regions may have different compliance requirements, data residency regulations, and network topologies. For example, some regions may have specific security certifications that may be required for certain types of data, while other regions may have restrictions on data transfer across geographic borders.

When creating roles and role assignments in RBAC, it is important to consider the region where your resources are located, and whether there are any specific access policies or requirements for that region. Some RBAC features, such as resource locks, can only be applied at the resource group or subscription level, and may not be supported across all regions.

To help manage RBAC across multiple regions, Azure provides several tools and features, such as Azure Policy and Azure Blueprints, that allow you to define and enforce policies and configurations across multiple subscriptions and regions. You can also use Azure Resource Manager templates to automate the deployment of RBAC configurations and resources across multiple regions.

Azure subscriptions assign various roles to users, thereby enabling them to manage and control resources. Roles such as Owner, Contributor, and Reader offer different levels of access and permissions. Subscriptions also act as boundaries for billing, usage monitoring, and resource quotas.

ome organizations look to further segment subscriptions by introducing additional workload layers, such as a sandbox environment or the split of non-production workloads into Test, User Acceptance Testing (UAT), Development, and Pre-Production.

 The shared space (hub) subscription would normally house the shared networking, identity, logic systems, and the like to be used between environments.

 Typically, when wanting to understand the full dynamics behind subscription design, you may want to read more around landing zone designs.

 <img width="1597" height="610" alt="image" src="https://github.com/user-attachments/assets/bf545a67-59bf-4388-b2db-7330442f949b" />

 For more information on subscriptions, please refer to the following URL: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/resource-org-subscriptions.

For more information on subscriptions in relation to landing zone designs, please refer to the following URL: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/resource-org-subscriptions.

Establish a dedicated connectivity subscription in your platform management group to host an Azure Virtual WAN hub, private Domain Name System (DNS), Azure ExpressRoute circuit, and other networking resources. A dedicated subscription ensures that all your foundation network resources are billed together and isolated from other workloads.

 Important

Subscriptions aren't tied to a specific region, and you can treat them as global subscriptions. They're logical constructs to provide billing, governance, security, and identity controls for Azure resources that are contained within them. Therefore, you don't need a separate subscription for each region.
A single subscription can contain resources from different regions, depending on the requirements and architecture.

In a subscription that contains resources from multiple regions, you can use resource groups to organize and contain resources by region.

Each Azure subscription is linked to a single Microsoft Entra tenant, which acts as an identity provider (IdP) for your Azure subscription. Use the Microsoft Entra tenant to authenticate users, services, and devices.

Use a shutdown schedule for nonproduction workloads to optimize costs.

Treat subscriptions as a unit of management that aligns with your business needs and priorities.

Billing Profiles
Billing profiles are part of the Azure Cost Management and Billing system, designed to help customers manage and track their Azure spending. A billing profile is a container for invoices, payments, and other billing-related information.

Azure Management Hierarchy
As organizations grow, managing Azure resources can become increasingly complex, especially with multiple departments, teams, or projects. Microsoft has designed a hierarchy of management that enables you to delegate control and assign responsibilities to different levels of your organization.

Management groups: Management groups provide a way to organize and manage subscriptions efficiently. They allow you to apply consistent policies and access control to multiple subscriptions, which can be particularly beneficial for organizations with complex structures or multiple Azure subscriptions. Management groups can be nested, allowing you to create a hierarchy that reflects your organization’s structure and needs.
Subscriptions: Azure subscriptions are agreements between Microsoft and a customer that grant access to Azure services and resources. Subscriptions can be used to manage resources, services, and costs within Azure, and they act as boundaries for billing, usage monitoring, and resource quotas. Subscriptions also allow you to assign user roles, which determine the level of access and permissions users have within the Azure environment.
Resource groups: Resource groups are logical containers for resources deployed within an Azure subscription. They provide a way to organize and manage resources based on their lifecycles and relationships with each other. Resource groups enable you to manage resources collectively, apply consistent policies, and provide access control.
Resources: Resources are individual Azure components, such as virtual machines, storage accounts, and databases. Resources are managed and organized within resource groups and subscriptions.
The hierarchy of management within Azure is defined as per Figure 3.2 below:

<img width="1521" height="637" alt="image" src="https://github.com/user-attachments/assets/d5a12746-3ccc-42e9-84a0-69025b2a1266" />

Key Considerations of the Hierarchy of Management for Enterprise Agreements
The Azure Enterprise Agreement (EA) management hierarchy consists of four main levels:

Enterprise: At the Enterprise level, the organization is identified by its Microsoft Entra tenant, and the layer at which the Azure agreement is defined (e.g., pay-as-you-go (PAYG), Cloud Solution Provider (CSP), also identified as an Azure Plan, or EA). This level serves as the identifier for your organization on Azure.
Departments: At the department level, sub-accounts are created for different organizational departments. Departments can be grouped functionally (e.g., IT and finance) or geographically (e.g., North America and Europe). A department owner can be added to manage the budget for the department.
Accounts: Within a department, multiple accounts can be created. Additional owners can be added to manage these accounts. When creating a personal account in Azure, this level serves as the starting point for creating subscriptions, with the Microsoft account used for Azure portal login added as the owner.
Subscriptions: Multiple subscriptions can be created within an account. This level is where billing occurs, and Azure resources are created. Additional subscription owners can be added to manage subscriptions, create resources, and assign users to a subscription. Subscriptions always maintain a trust relationship with a Microsoft Entra instance.

<img width="1337" height="680" alt="image" src="https://github.com/user-attachments/assets/47dce4a0-f481-4572-885d-7184ea07c2ca" />


Azure subscriptions have trust relationships associated with Microsoft Entra. Through this trust, a subscription enables Microsoft Entra ID to authenticate users, services, and devices.

A Microsoft Entra tenant can have a 1:M (one to many) relationship with subscriptions (meaning it can be associated with multiple subscriptions), but a subscription can only have a 1:1 relationship with a tenant (meaning one subscription can only be associated with one tenant).


<img width="1559" height="696" alt="image" src="https://github.com/user-attachments/assets/b570159f-5b7d-4790-9ba8-e6dccb42a12d" />

Why Have Multiple Subscriptions in an Environment?
This is part of the organizational strategy when defining Azure, and it’s important to understand the segregation of data and resources and how this will be managed perpetually by the business. Some motivations to split out resource groups are separating resources by the following:

Different business units (BUs) (Finance/IT/Marketing)
Different environments (Dev/Test/UAT/PROD)
Geographic (West Europe/Central US)
Cost centers (could be the same as BUs or a unique code)


When defining governance around Azure, it’s important to define a naming convention that will be applied across multiple layers, including subscriptions. It’s recommended to identify a subscription location and purpose in the name—for example, WE_PROD. We advise that you carefully consider a landing zone design when contemplating subscriptions. 

Initial subscription strategy: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/initial-subscriptions

Multi-subscription strategy: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/scale-subscriptions

You can read more here: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/.

Configuring Management Groups
Azure management groups help you organize your resources and subscriptions and sit above the subscription layer, which allows global governance of the Azure platform.

Subscriptions are organized into containers called management groups that allow a transitive flow of common conditions through subscription layers, such as Azure policies and RBAC permissions. This structure should always dictate a form of logical hierarchy structure that should be constructed to allow a flow of permissions or policies as required by the organization.

<img width="1262" height="574" alt="image" src="https://github.com/user-attachments/assets/beb29a9b-0232-4b04-824e-57b60392c7a6" />

Remember that the permission structure could be loosely defined at the subscription layer but is more appropriately defined at the level that allows the most restrictive access and only access to what is required.

<img width="1228" height="388" alt="image" src="https://github.com/user-attachments/assets/936fd194-88f9-448b-b911-3f2a330bb22c" />

Organizing subscriptions: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/organize-subscriptions

Management groups documentation: https://learn.microsoft.com/en-us/azure/governance/management-groups/

Management group structures within a Microsoft Entra tenant support organizational mapping. Consider your management group structure thoroughly when your organization plans its Azure adoption at scale.

Determine how your organization separates out services that specific teams own or operate.

Determine whether you have specific functions that you need to keep separate for reasons like business requirements, operational requirements, regulatory requirements, data residency, data security, or data sovereignty compliance.

Use management groups to aggregate policy and initiative assignments via Azure Policy.

Enable Azure role-based access control (RBAC) authorization for management group operations to override the default authorization. By default, any principal, like a user principal or service principal, within a Microsoft Entra tenant can create new management groups. For more information, see How to protect your resource hierarchy.




The first management group in Azure is the Tenant Root Group—this is created by default and is the top parent group; all subsequent management groups will fall as child management groups under the root group. Also, the root group cannot be deleted.

Also consider the following factors:

A management group tree can support up to six levels of depth. This limit doesn't include the tenant root level or the subscription level.

All new subscriptions are placed under the tenant root management group by default.

 Instead, use management groups to assign Azure policies and initiatives that apply to all subscriptions in the management group that require the same security, governance, and compliance settings.

 <img width="1600" height="608" alt="image" src="https://github.com/user-attachments/assets/4f293c3c-440a-4eaf-b688-495ce455dc90" />

 <img width="1988" height="673" alt="image" src="https://github.com/user-attachments/assets/c6950042-783e-4ca1-81f4-1edba8cb471c" />

 Understanding role-based-access-control
Azure Role-Based Access Control (RBAC) is a tool that’s used to manage access to Azure resources. It provides fine-grained control over who can perform specific actions (such as creating, updating, or deleting resources) on specific resources within an Azure subscription. With Azure RBAC, you can grant permissions to users, groups, and applications, which is defined as the scope, such as a management group, subscription, resource group, or individual resource. This way, you can ensure that users have the necessary permissions to perform their tasks, while preventing them from accessing resources that they do not need.

To use Azure RBAC, you need to have an Azure subscription and a Microsoft Entra tenant. You can then assign roles to users, groups, or applications within the Azure portal or by using Azure PowerShell or the Azure CLI.

RBAC built-in Roles
Azure RBAC includes built-in roles such as Owner, Contributor, and Reader, as well as custom roles that you can define yourself. 

Owner role: This is the role that includes all permissions related to management; you can read, add, and remove resources. You also have the capability to add and remove other users to and from resources as owners or other roles.
Contributor role: This role has the same permissions as an owner, except you cannot add or remove additional users to and from resources.
Reader role: This role has the ability to view resources but cannot amend, add, or remove users or resources.

There are multiple built-in roles within Azure, and it is recommended that you have a look at them to learn more: https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles.






