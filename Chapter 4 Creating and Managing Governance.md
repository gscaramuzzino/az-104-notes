Chapter 4 Creating and Managing Governance

This chapter covers how to establish governance in Azure and create mechanisms for managing it. In this chapter, you will learn how to create Azure policies and why they exist. You will also learn how to apply and manage resource tags.

In this chapter, you are going to learn about the following main topics:

Understanding Azure policies
Applying and Managing Tags on Resources

Azure Policies

Azure Policy is a mechanism for effecting organizational compliance on the Azure platform. The service allows aggregated views to understand the overall state of an environment, with the ability to view resource-level granularity for compliance. All this can be viewed on the compliance dashboard as part of the Policy service. Remediation can be applied automatically and through bulk operations.

Azure Policy helps maintain consistency across the entire cloud environment, improve security posture, and achieve greater operational efficiency.

Some key features of Azure Policy include the following bulleted items, which will be explored in more detail in the sections ahead:

Policy definition: Users can create custom policies using Azure Policy definition language (a JavaScript Object Notation (JSON)-based format) or choose from a library of built-in policy definitions provided by Azure
Policy assignment: Policies can be assigned to specific resources, resource groups, or entire subscriptions, allowing for granular control over policy enforcement
Policy evaluation: Azure Policy continuously evaluates the assigned policies against the existing resources and identifies any non-compliant resources
Remediation: In certain cases, Azure Policy can automatically remediate non-compliant resources by applying the required changes to bring them into compliance
Compliance reporting: Azure Policy provides comprehensive compliance reporting, enabling users to track the compliance status of their resources and identify any issues that need to be addressed
Integration: Azure Policy can be integrated with Azure DevOps, Azure Security Center, and Azure Monitor to enhance governance, security, and monitoring capabilities across the cloud environment
Overall, Azure Policy is an essential tool for organizations that want to maintain control over their Azure resources, ensuring they adhere to the necessary governance, risk, and compliance requirements.

Azure Policy assesses compliance by comparing resource properties to business rules defined in JSON format. These are known as policy definitions.

A policy initiative is a grouping of definitions that align with business objectives, such as the secure configuration of virtual machines (VMs). This could contain a policy to assess antivirus compliance and a policy for assessing disk encryption compliance, as well as other policies.

<img width="1279" height="560" alt="image" src="https://github.com/user-attachments/assets/43a2878f-68b9-4b2c-9477-f4a205a0b1f1" />


Azure Policy focuses on resource properties for existing resources and resources being deployed. Azure Policy is used for the enforcement of governance standards within the Azure platform.
RBAC focuses on user actions at different scopes. RBAC contributes to governance by enforcing permissions at the service principal layer.

Some examples of built-in policies are the following:

Allowed virtual machine size SKUs: This policy specifies a set of VM sizes and types that can be deployed in Azure.
Allowed locations: This policy restricts available locations where resources can be deployed.
Allowed resource types: This policy defines a list of resource types that can be deployed. Resource types that are not on the list can’t be deployed inside the Azure environment.
Not allowed resource types: This policy prevents certain resource types from being deployed.
Require a tag and its value on resources: This policy enforces a required tag and its value. It does not apply to resource groups.
Microsoft maintains a repository of policies at the following GitHub link: https://github.com/Azure/azure-policy. This can be handy for starting new policy templates that you want to build and understanding how the native policies are constructed.


Constructing a Policy Definition
In the following section, you will explore the structure of a policy definition. The policy definition is what describes how a policy looks and behaves. In order for you to effectively work with policies, it is important that you maintain a core understanding of the components they contain. They are constructed of the following key components:

displayName: This is the display name of the policy file.
Description: This is a descriptor field that allows you to add a small write-up on the desired effect and scope of the policy.
Effect: Several effects can be applied to policies. It’s important to note that this is typically for logical evaluation (if, then), which belongs to the policy rule. To understand these effects in more detail, please refer to the following Microsoft Uniform Resource Locator (URL): https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effects.
Category: This defines the category type of your policy.
Location: This defines the location of the policy to be deployed.
ID: This is the definition identifier (ID) of the policy that is created and is enumerated based on the policy name.
Type: This defines the policy type to be implemented and can be a Built-in, Custom, or Static policy type.
Mode: This is used to define whether a policy is scoped toward a resource provider or Azure Resource Manager (ARM) property.

The different effect types are described as follows:

Append: This is used to modify existing or new resources by adding additional fields or properties to a resource.
Audit: This is used to flag a resource that is not compliant. It notes the non-compliance but will not restrict the deployment request.
AuditIfNotExists: This is used to identify resources identified within the policy’s (or policies’) scope that are missing the required properties for the resource type.
Deny: This is used to disallow the deployment of resources that do not meet the policy definition criteria.
DeployIfNotExists: This is used to perform a template deployment when non-compliance is met, as described in the AuditIfNotExists policy criteria.
Disabled: This is used to nullify the effect of a policy and is typically used for testing scenarios.
Modify: This is used to modify the properties of resources and will apply to new and existing resources that meet the policy criteria. Resources can be remediated through a remediation task.

<img width="1650" height="1485" alt="image" src="https://github.com/user-attachments/assets/d26cd98a-6b87-4726-bf22-8531676a7c7e" />

Groups help you organize policies within an initiative.
Remember that definitions are a guideline set of rules that are assessed, and parameters are the values to assess for.

Azure Polcies not applied on Resource groups.

 Note that newly applied policies may take several minutes to be applied, as well as for compliance to be reflected. Typically, policies take about 30 minutes to apply, while compliance runs once every 24 hours.

 <img width="1650" height="807" alt="image" src="https://github.com/user-attachments/assets/931855c5-b66b-4bce-b44b-ced0d78ed7b8" />

Resource compliance describes resource adherence to the defined policies to which they are applicable. Policy compliance can exist in three different states, as outlined here:

Compliant: A resource conforms to defined policy standards.
Non-compliant: A resource does not conform to the required policy standard.
Exempt: A resource has been identified to be exempt from the policy evaluation. This is explicitly defined for an exemption or can’t be evaluated. Exempt resources will still be evaluated in the total compliance rating score.

Policies can be used in conjunction with tags to effect compliance in an organization.

Applying and Managing Tags on Resources
Tags in Azure are metadata labels that can be assigned to resources, resource groups, and subscriptions to help users organize, categorize, and manage their cloud resources more effectively. Tags are key-value pairs that provide additional information about the resources and can be used for various purposes, such as tracking ownership, managing cost allocation, and enforcing governance policies. Here are some reasons why organizations may want to use tags in Azure:

Organization: Tags help users organize their resources based on specific criteria, such as project, environment, or department. This makes it easier to manage and locate resources within a complex cloud environment.
Cost management: By tagging resources with relevant cost center, project, or department information, organizations can more accurately track and allocate costs associated with their cloud resources.
Governance and compliance: Tags can be used in conjunction with Azure Policy to enforce governance rules and ensure that resources comply with organizational standards. For example, a policy can require that all resources have specific tags assigned, such as owner and expiration date.
Automation: Tags can be utilized in automation scripts or templates to filter resources based on specific criteria, streamlining operations and management tasks.
Reporting and monitoring: Tags can be used in reporting and monitoring tools, such as Azure Cost Management or Azure Monitor, to create custom dashboards and reports based on specific resource groupings.
In summary, tags in Azure provide a flexible and powerful way to organize, manage, and track cloud resources, enabling organizations to maintain better control over their cloud environment and optimize resource usage, costs, and compliance.

Tag names are case-insensitive and tag values are case-sensitive.

Some important common tag patterns are noted here:

Functional: Classification of resources by defining the functionality the resource(s) introduces to the workload environment. Here are examples of functional tags:
Application name: Use this to classify a set of resources for an application
Environment: DEV/TEST/UAT/STAGING/PROD/DR
Classification: This tag can be used to describe data classification pertaining to resources. This is particularly valuable for compliance alignment, such as with the General Data Protection Regulation (GDPR). The following is an example of a classification tag:
Confidentiality: Private/Public/Restricted
Accounting: This set of tags is particularly focused on cost governance and the assignment of resource(s) to a billing unit/entity within the organization. The following are examples of accounting tags:
Department: Finance/IT/HR/Marketing/Sales
Region: West Europe/Central US, and so on
Partnership: This set of tags is used to identify people in the organization who can or should be contacted as they contain relevance to the resource. The following are examples of partnership tags:
Owner: Identify the product owner for the service
Support email: Identify who to contact when support is needed
Business criticality: Define how important the resource is to the business (normally a metric value such as BC1/BC2/BC3)
SLA objectives: Define a service-level agreement (SLA) tier that would apply to determine the support required for the service (for example, SLA Tier 1/SLA Tier 2/SLA Tier 3)
Purpose: This set of tags is reserved for understanding the key deliverable for the application and is aligned with a business objective. Here is an example of a purpose tag:
Purpose: Describe the application’s purpose in a single line. This assists later in troubleshooting by providing a basic understanding of what the application is and what it does.

The replace command switch will remove tags that are not present in the $tags variable. The merge command will amend tags that are present and add any missing tags defined in the $tags variable.

You are encouraged to read up further by using the following links:

Microsoft documentation on tags: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources?tabs=json

Resource naming and tagging decision guide: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming-and-tagging-decision-guide?toc=%2Fazure%2Fazure-resource-manager%2Fmanagement%2Ftoc.json

Prescriptive guidance for resource tagging: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/guides/complex/prescriptive-guidance#resource-tagging

Applying tags in PowerShell: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources?tabs=json#powershell



