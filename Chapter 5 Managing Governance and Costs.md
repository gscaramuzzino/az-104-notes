Chapter 5 Managing Governance and Costs

In this chapter, you are going to explore the following main topics:

Managing resource groups
Configuring resource locks
Managing costs

Resource groups are logical containers for grouping multiple resources together. Resources can be virtual machines (VMs), databases, virtual networks, web apps, and so forth. A resource group should group all resources that have a similar or the same life cycle—for instance, all items that are deployed, updated, or deleted with some form of commonality, such as belonging to the same application, service, type, department, or location.

Some important points to note when defining resource groups are outlined here:

A resource can only belong to a single resource group at any time.
Resources can be added and removed from a resource group at any time.
Resource group metadata (the data describing the resource group and resources) is stored in the region where the resource group is created.
Resources in a resource group are not bound by the location defined for the resource group and can be deployed into different regions.
If a resource group’s region is unavailable, you cannot update, modify, or delete any resources in the group due to the metadata being unavailable. Resources in other regions will continue to function as expected, even in the resource group.
Access control actions can be associated with resource groups through role-based access control (RBAC) roles, Azure Policy, or resource locks.

Consider a resource group organization strategy when creating resource groups, to identify ownership, billing, location, resource type, department, applications, and access.

Resource group names must be unique per subscription.

 Also, in situations where you may find yourself needing to delete a collection of resources at once that all reside in a resource group, deleting the resource group can be a very effective method of removing these at all at once.

 One of the great things about the Move options available in Azure is that no downtime is incurred on those resources. If you had to move a VM, you would be surprised to note that you would lose no pings to the VM if you ran a continuous ping while moving the resources. This can be very helpful when performing this for your company or customers.

 The following URL will assist in considering items before moving: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/move-resource-group-and-subscription#checklist-before-moving-resources

Not all resources support migrations, and the following up-to-date link will provide supported operations by resource type: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/move-support-resources

You are encouraged to read up on this further by using the following links:

Managing resource groups: https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal

Moving resources to other resource groups or another subscription: https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/move-resource-group-and-subscription

PowerShell Scripts
This section introduces PowerShell scripts that can be used for the automation of resource group management, as well as for quicker administration times. Please ensure that the Az module is installed, as per the Technical Requirements section at the beginning of the chapter. Then, proceed as follows:

Create a new empty resource group. Define a location and name for the new resource group to be deployed, as follows:

New-AzResourceGroup -Name RG01 -Location "West Europe"
Create another new empty resource group with tags. Define a location, a name, and tags for the resource group, as follows:

$tags = @{"Tag1"="Value1"; "Tag2"="Value2"}
New-AzResourceGroup -Name RG02 -Location "West Europe" -Tag $tags

Azure resource locks are a security feature that helps prevent the accidental modification or deletion of resources in an Azure subscription. These locks can be applied to various resources, such as VMs, storage accounts, and databases. There are two types of resource locks:

ReadOnly: This lock allows you to view the resource but prevents any modifications or deletions. It ensures that the resource remains in its current state and is not accidentally altered. It grants authorized users the read permissions to resources only. This means that they can’t add, delete, or modify resources. The effect is similar to the Reader role in RBAC.

CanNotDelete: This lock allows you to view and modify the resource but prevents it from being deleted. This is useful for protecting critical resources from accidental deletion.

In summary, locks can be applied to multiple layers (the subscription, resource group, or even at a resource level) and will prevent other administrators from modifying or deleting the resources. You also can apply different types of locks, such as ReadOnly and CanNotDelete. Restrictions applied through management locks will apply across all users and roles.

When applying locks, it’s important to understand that the precedence assigned is based on the most restrictive lock that is inherited.

It is important to note that when applying resource locks, the law of inheritance applies, meaning that all resources inherit the lock from the parent scope. The parent scope will be from the highest level of resources in the Azure hierarchy to the resource level, meaning that you can go from subscription down to resource groups down to resources; the parent will be the level at which the lock is applied.

Built-In Azure Roles
If your preference is to use a predefined Azure role, then either of the following will be suitable: Owner or User Access Administrator

Custom RBAC Roles
If your preference is to define or update a custom role, then the following action permissions are required:

Microsoft.Authorization/*
Microsoft.Authorization/locks/*

Applying a Resource Lock to a Resource
In order to apply a lock to a resource, you will need to provide the name of the resource, its resource type, and its resource group name, as in the following script:


New-AzResourceLock -LockLevel CanNotDelete -LockName DontDeleteProd -ResourceName ProductionWebApp -ResourceType Microsoft.Web/sites -ResourceGroupName ProdNorthEuropeRG
Now, let’s try the same for a resource group.

Applying a Resource Lock to a Resource Group
To lock a resource group, provide the name of the resource group and the type of lock to be applied using the following script:


New-AzResourceLock -LockName LockDeleteQA -LockLevel CanNotDelete -ResourceGroupName QualityAssuranceRG
This applies the resource lock to the resource group successfully.

Viewing Resource Locks in Effect
To get information about a lock, use the Get-AzResourceLock cmdlet. To get all locks in your subscription, use the following command:

Get-AzResourceLock

Exam Tip

One important exam tip is to always check restrictions to prevent unexpected behaviors, such as locks preventing backup. See the following page for more information on this: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources?tabs=json#considerations-before-applying-locks.

ou are encouraged to read up further by using the following link:

Microsoft documentation for resource locks: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources?

The following link will provide some references to situations where you might want to apply resource locks within your Azure Blueprints:

Resource locks in Azure Blueprints: https://learn.microsoft.com/en-us/azure/governance/blueprints/concepts/resource-locking

Azure Cost Management + Billing is a suite of tools designed to assist in the analysis, management, and cost optimization of Azure workloads. It assists in the following management tasks relating to costs:

Billing administration tasks
Managing billing access
Reports on cost and usage data
Configuration of budgets
Identifying opportunities to optimize costs

Cost Management
Cost management contains many facets and should be considered in its entirety; this includes cost analysis, governance, and reporting. For the purpose of the exam, we will investigate cost analysis and report scheduling.

Cost Analysis
Cost analysis assists in understanding expenditure within Azure. Quick reports are automatically generated to provide insights into current and historical expenditures on the scope chosen. Further to understanding current costs, the utility predicts anticipated forecast expenditure for the month ahead.

Costs can also be exported for viewing in Portable Network Graphics (PNG), Excel, and comma-separated values (CSV) format by clicking on the Download button

Scheduled Reports
<img width="1650" height="593" alt="image" src="https://github.com/user-attachments/assets/9479b16e-c0e5-4d2d-8adc-fdf21549eb38" />

<img width="1650" height="1086" alt="image" src="https://github.com/user-attachments/assets/f9134551-9e1b-484f-9b55-36e30170396e" />

Budgets
In Azure, budgets are an essential component of Cost Management, allowing organizations to set spending limits and monitor their cloud expenses. Budgets in Azure consist of several components that help define and manage the financial constraints of your cloud usage:

Scope: The scope defines the level at which the budget is applied. It can be set at the subscription, resource group, or management group level. By selecting the appropriate scope, you can create budgets for specific projects, departments, or the entire organization.
Time frame: Budgets in Azure can be set for different durations, such as monthly, quarterly, or annually. This allows you to track spending over various periods and align the budget with your financial reporting cycles.
Amount: The amount represents the spending limit for the defined scope and time frame. Once the budget is set, Azure will track the costs incurred within the selected scope and notify you when specific thresholds are reached.
Cost filters: You can apply filters to your budgets based on resource types, locations, services, or tags. This allows you to create more granular budgets that focus on specific areas of your cloud environment.
Alert thresholds: Alert thresholds are percentage values that trigger notifications when your spending reaches a certain level relative to your budget. For example, you can set alerts at 50%, 75%, and 90% of the budget to receive timely updates about your spending progress and take necessary actions to stay within the budget limits.
Notification recipients: Budgets in Azure allow you to specify email recipients for the budget alerts. By adding appropriate stakeholders, you can ensure that the right people are informed about the budget status and any potential cost overruns.


<img width="1234" height="1063" alt="image" src="https://github.com/user-attachments/assets/29a8c8e6-f596-4ab4-9368-425459b3daf5" />

<img width="1650" height="187" alt="image" src="https://github.com/user-attachments/assets/f7fc4a9d-56eb-4561-95c4-72d4a0faa60c" />

lert Recipients (Email):

This typically refers to the individuals or groups who receive email notifications when an alert is triggered. These recipients are specified directly in the alert configuration.
The email notifications are sent to inform the recipients about the alert, allowing them to take necessary actions based on the alert details.
Email/SMS Push Notifications as Action Groups:

Action groups are collections of notification preferences and actions that are triggered when an alert is fired. They are more versatile and can include multiple types of notifications and actions.
An action group can include email notifications, SMS messages, push notifications, voice calls, and even automated actions like triggering a webhook or Azure Function.
Action groups are reusable across multiple alert rules, meaning you can define a set of actions once and apply them to different alerts as needed.

Cost Alerts
Cost alerts enable notifications for identified alert trigger points that are configured for an environment. You can create these for resources or resource groups that exceed an expected expenditure or when you are getting close to a threshold.

To modify an existing alert, you will need to modify the budget settings. To do so, perform the following steps:

Advisor Recommendations
Advisor automatically detects cost optimizations that can be implemented within the tenant. While the recommendations are particularly good and will absolutely lead to cost savings, review each item and confirm where costs can be further reduced through an understanding of resources within the Azure environment. Right-sizing is critical for managing costs and is highly advised as the first exercise to be conducted before considering reserved instances and capacity.

Reservations
Reservations are a mechanism for saving money on Azure by committing to one-year or three-year plans for resources. Through this, you receive a significant discount from Microsoft, up to 72% compared to pay-as-you-go prices. Reservations must be carefully planned as they are long-term investments and are applied at stock-keeping unit (SKU), scope, and sometimes region levels. Reservations do offer some form of flexibility (especially when applied to VMs) but are limited in nature, particularly on the same family of VMs where a ratio will be applied when the applicable SKU is not found.

If the organization you are working with has subscribed to an Enterprise Agreement with Microsoft and has subscribed to Software Assurance, cost-savings can be leveraged on VMs by enabling Azure hybrid benefit on the VM properties page.

You are encouraged to read up further by using the following links:

Transfer billing ownership of a subscription: https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/billing-subscription-transfer

Cost Management overview: https://learn.microsoft.com/en-gb/azure/cost-management-billing/cost-management-billing-overview

Cost Management best practices: https://learn.microsoft.com/en-gb/azure/cost-management-billing/costs/cost-mgt-best-practices

Azure reservations: https://learn.microsoft.com/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations

