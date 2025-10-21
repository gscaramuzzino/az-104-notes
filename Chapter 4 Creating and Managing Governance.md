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


https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781805122852/files/image/B20834_04_02.jpg

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


