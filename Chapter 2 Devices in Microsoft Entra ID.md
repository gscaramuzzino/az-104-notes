In this chapter, the following topics will be covered:

- Configuring and Managing Devices
- Configuring Microsoft Entra Join
- Performing Bulk Operations
- Navigating Guest Accounts
- Configuring SSPR


## Configuring and Managing Devices

In Microsoft Entra, a device represents any physical or virtual device that is registered with the directory. This can include devices such as laptops, desktops, mobile phones, and tablets. When a device is registered with Microsoft Entra, it can be managed and secured using policies and configurations defined in the directory. By managing devices in Microsoft Entra, IT administrators can ensure that devices accessing corporate resources meet an organization’s security and compliance requirements.

### Microsoft Entra Device Registration

A Microsoft Entra ID Registered Device is one that is registered within the Microsoft Entra ID directory but not added as a member of an organization:

- The device is then granted access to resources through an attachment to a Microsoft account in Microsoft Entra ID.
- It provides users with a Single Sign-On (SSO) experience across their devices, including app authentication.
- It enables Conditional Access policy enforcement.
- It is recommended for personally owned devices or devices not used exclusively for business purposes. Personally owned devices are also defined as BYOD, which are devices that can be used for work purposes.
- It offers a streamlined process with minimal administrative overhead.
- The device can be managed through tools such as Microsoft Intune.

The following diagram illustrates a device’s connection to Microsoft Entra ID and the relationship flow.

<img width="1650" height="359" alt="image" src="https://github.com/user-attachments/assets/27ddbb07-1d38-412b-b6e0-6ff495d88428" />

For more details, refer to https://learn.microsoft.com/en-us/entra/identity/devices/concept-device-registration.

### Microsoft Entra Join

A Microsoft Entra ID joined device is one that is added to an organization’s Microsoft Entra ID directory, providing additional benefits and control to the organization:

- It is fully managed by the organization with access to on-premises Active Directory resources. It is, therefore, suitable for dedicated, organization-owned devices that need full access to organizational resources.
- It is explicitly tied to an organizational user account and managed as part of the directory.
- It offers better management capabilities and integration and can use Conditional Access policies.

<img width="1650" height="508" alt="image" src="https://github.com/user-attachments/assets/82e818a3-f5de-4fc4-8a19-250675eaa0dd" />

For more details, refer to https://learn.microsoft.com/en-us/entra/identity/devices/concept-directory-join.

### Microsoft Entra Hybrid Join

A Microsoft Entra ID hybrid joined device is a device that is joined to both the on-premises Active Directory (AD) and Entra ID, for organizations with a blended infrastructure. It is designed to support Windows 10 and 11 devices:

- It retains the benefits of local on-premises AD while leveraging cloud features, such as enabling the continued use of Group Policy in Entra ID
- It combines cloud authentication with on-premises resources and devices
- It facilitates seamless transitions and secure access to resources in hybrid environments
- It is ideal for organizations that have a mix of cloud and on-premises infrastructure deployments

The following diagram illustrates a device connection to Microsoft Entra ID and the relationship flow for a Microsoft Entra ID hybrid join connection, demonstrating how the connection is made from the device to Microsoft Entra ID as a registration and to an Active Directory for a domain join. Entra ID will then have a hybrid connection to an on-premises Active Directory system, with synchronization occurring between the platforms through the Microsoft Entra Connect service

<img width="1650" height="785" alt="image" src="https://github.com/user-attachments/assets/dd360a8e-c99a-4913-ba3b-86956780c073" />

For more details, refer to https://learn.microsoft.com/en-us/entra/identity/devices/concept-hybrid-join.

## Device Settings

Microsoft Entra enables organizations to ensure that their users access Azure resources from devices that comply with their security and compliance policies. Device management is a crucial component of device-based Conditional Access, where access to corporate resources is restricted only to managed devices.

Key device settings and controls:

- Users may join devices to Microsoft Entra
- Users may register their devices with Entra ID
- Require Multi-Factor Authentication to register or join devices with Microsoft Entra
- Maximum number of devices per user
- Manage additional local administrators on all Microsoft Entra joined devices
- Enable Microsoft Entra Local Administrator Password Solution (LAPS): Local Administrator Password Solution (LAPS)
- Restrict users from recovering the BitLocker key(s) for their owned devices

## Enterprise State Roaming

Enterprise State Roaming is a feature in Microsoft Entra ID that allows users to synchronize their application and system settings across their Windows devices. This means that when a user sets up a new Windows device, their familiar settings and preferences will be applied to the new device automaticall

## Device Audit Logs

The audit logs section under Devices in Microsoft Entra ID contains a record of all activities related to device management. Audit logs provide detailed information on events and actions performed within the system. These logs offer valuable insights for administrators looking to monitor security, troubleshoot issues, and maintain compliance.

## Microsoft Entra ID offer plans

| Plan | Description |
|---|---|
| Microsoft Entra ID Free | This offers the most basic features, such as support for SSO across Azure, Microsoft 365, and other popular Software as a Service (SaaS) applications, Azure Business-to-Business (B2B) for external users, support for Microsoft Entra Connect synchronization, self-service password change, user and group management, and standard security reports. |
| Microsoft Entra ID P1 | Previously known as Azure Active Directory P1. In addition to the Free license features, this license offers a service-level agreement, advanced reporting, Conditional Access, Microsoft Entra Connect Health, advanced administration such as dynamic groups, self-service group management, and Microsoft Identity Manager. |
| Microsoft Entra ID P2 | Previously known as Azure Active Directory P2. In addition to the Free and Microsoft Entra ID P1 license features, the Microsoft Entra ID P2 license includes Identity Protection, Privileged Identity Management (PIM), access reviews, and entitlement management. |
| Microsoft Entra ID Governance | For users of Microsoft Entra ID P1 and P2, Microsoft Entra ID Governance provides a sophisticated suite of identity governance features that can be added at a premium. These capabilities include automated user and group provisioning, HR-driven provisioning, terms of use attestation, basic and advanced access certifications and reviews, basic and advanced entitlement management, life cycle workflows, identity governance dashboard, and PIM. |
| Microsoft Entra Verified ID | Microsoft Entra Verified ID is a license currently included free within any Microsoft Entra ID subscription, such as Microsoft Entra ID Free. This service enables organizations to verify and issue credentials based on unique identity attributes, granting individuals control over their digital credentials and improving visibility. The benefits of Verified ID include reduced organizational risk, simplified audit processes, and seamless integration for developers to create user-centric serverless applications. Organizations can enable Verified ID for free in the Microsoft Entra admin center. |
| Microsoft Entra Permissions Management | This is a set of identity governance features tailored for Microsoft Entra ID P1 and P2 subscribers. These capabilities include automated user and group provisioning, HR-driven provisioning, terms of use attestation, basic and advanced access certifications and reviews, basic and advanced entitlement management, life cycle workflows, identity governance dashboard, and PIM. |
| Microsoft Entra Workload ID | With the standalone Microsoft Entra Workload ID product, organizations can reduce risk exposure from compromised or lost identities or credentials, regulate workload identity access with adaptive policies, and obtain a thorough workload identity health-check view. The monthly pricing for Workload ID is based on the workload identity. |

## Configuring Microsoft Entra Join

With Microsoft Entra Join, you can join devices directly to Microsoft Entra without the need to join your on-premises Active Directory in a hybrid environment. While Microsoft Entra hybrid join with an on-premises Active Directory might still be preferred for some scenarios, Microsoft Entra Join simplifies the process of adding devices and modernizes device management for your organization. This can result in the reduction of device-related IT costs.

Your users may have access to corporate assets through their devices. To protect these corporate assets, you want to control these devices. This allows your administrators to ensure that your users are accessing resources from devices that meet your standards for security and compliance.

Microsoft Entra Join is a good solution when you want to manage devices with a cloud device management solution, when you want to modernize your application infrastructure, when you want to simplify device provisioning for geographically distributed users, and when your company adopts Microsoft 365 as the productivity suite for your users.

### Microsoft Entra Join Methods

Microsoft Entra Join can be employed through any of the following methods:

- Bulk deployment: This method is used to join large numbers of new Windows devices to Microsoft Entra and Microsoft Intune.
- Windows Autopilot: This is a collection of technologies used to preconfigure Windows 10 and later devices so that the devices are ready for productive use. Autopilot can also be used to reset, repurpose, and recover devices.
- Self-service experience: This is also referred to as a first-run experience, which is mainly used to join a new device to Microsoft Entra.

## Performing Bulk Updates Using the Azure Portal

Performing bulk user updates is like managing single users (such as internal and guest users). The only property that can’t be set for multiple users is resetting a password, which must be done for a single user.

Azure has also improved its bulk user settings by adding a drop-down menu that enables you to perform updates via the downloadable CSV template, which you then re-upload.

<img width="1650" height="469" alt="image" src="https://github.com/user-attachments/assets/f30b8f69-f379-49f9-9253-a461be94e5cb" />

Navigating Guest Accounts
In Microsoft Entra ID, a guest account is a user account that is created in one Microsoft Entra directory, allowing a user from another Microsoft Entra directory, or an external identity provider, to access resources in the first tenant. Guest accounts can be invited to access applications, groups, or resources by users with appropriate permissions in the inviting tenant. This feature enables organizations to collaborate and share resources with external partners, contractors, or customers while maintaining control over their own corporate data. Guest users have limited access to Microsoft Entra ID resources, and their permissions can be managed and revoked by the inviting organization.

Configuring SSPR
Microsoft Entra ID SSPR allows users to reset their own passwords without the need to contact IT support or administrators. With SSPR, users can verify their identity using different methods, such as email, text message, or a mobile app notification, and reset their password without any help. This feature is not only convenient for end users but also reduces the workload for IT support, increases security by ensuring that users have strong passwords, and saves time and resources. SSPR is an essential feature for any organization that wants to improve user productivity and reduce IT costs.

Configuring SSPR
Microsoft Entra ID SSPR allows users to reset their own passwords without the need to contact IT support or administrators. With SSPR, users can verify their identity using different methods, such as email, text message, or a mobile app notification, and reset their password without any help. This feature is not only convenient for end users but also reduces the workload for IT support, increases security by ensuring that users have strong passwords, and saves time and resources. SSPR is an essential feature for any organization that wants to improve user productivity and reduce IT costs.

There are several things to keep in mind when considering implementing this feature in your organization:

Firstly, SSPR requires a Microsoft Entra ID account with Global Administrator privileges to manage SSPR options. This permission will allow the user to always be able to reset their own passwords, no matter what options are configured.
Additionally, SSPR uses a security group to limit the users who have SSPR privileges, providing an added layer of security to the feature.
It’s important to note that all user accounts in your organization must have a valid license to use SSPR. This means that if your organization has licenses for Office 365 or Microsoft Entra P1 or P2, you can enable SSPR for all users. If not, you must purchase Microsoft Entra P1 licenses to enable SSPR for your users.

The Microsoft Entra free-tier license only supports cloud users for SSPR, and only password change is supported, not a password reset.




