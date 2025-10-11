In this chapter, the following topics will be covered:

Configuring and Managing Devices
Configuring Microsoft Entra Join
Performing Bulk Operations
Navigating Guest Accounts
Configuring SSPR


Configuring and Managing Devices
In Microsoft Entra, a device represents any physical or virtual device that is registered with the directory. This can include devices such as laptops, desktops, mobile phones, and tablets. When a device is registered with Microsoft Entra, it can be managed and secured using policies and configurations defined in the directory. By managing devices in Microsoft Entra, IT administrators can ensure that devices accessing corporate resources meet an organization’s security and compliance requirements.

Microsoft Entra Device Registration
A Microsoft Entra ID Registered Device is one that is registered within the Microsoft Entra ID directory but not added as a member of an organization:

The device is then granted access to resources through an attachment to a Microsoft account in Microsoft Entra ID.
It provides users with a Single Sign-On (SSO) experience across their devices, including app authentication.
It enables Conditional Access policy enforcement.
It is recommended for personally owned devices or devices not used exclusively for business purposes. Personally owned devices are also defined as BYOD, which are devices that can be used for work purposes.
It offers a streamlined process with minimal administrative overhead.
The device can be managed through tools such as Microsoft Intune.
The following diagram illustrates a device’s connection to Microsoft Entra ID and the relationship flow.

<img width="1650" height="359" alt="image" src="https://github.com/user-attachments/assets/27ddbb07-1d38-412b-b6e0-6ff495d88428" />

For more details, refer to https://learn.microsoft.com/en-us/entra/identity/devices/concept-device-registration.

Microsoft Entra Join
A Microsoft Entra ID joined device is one that is added to an organization’s Microsoft Entra ID directory, providing additional benefits and control to the organization:

It is fully managed by the organization with access to on-premises Active Directory resources. It is, therefore, suitable for dedicated, organization-owned devices that need full access to organizational resources.
It is explicitly tied to an organizational user account and managed as part of the directory.
It offers better management capabilities and integration and can use Conditional Access policies.

<img width="1650" height="508" alt="image" src="https://github.com/user-attachments/assets/82e818a3-f5de-4fc4-8a19-250675eaa0dd" />

For more details, refer to https://learn.microsoft.com/en-us/entra/identity/devices/concept-directory-join.

Microsoft Entra Hybrid Join
A Microsoft Entra ID hybrid joined device is a device that is joined to both the on-premises Active Directory (AD) and Entra ID, for organizations with a blended infrastructure. It is designed to support Windows 10 and 11 devices:

It retains the benefits of local on-premises AD while leveraging cloud features, such as enabling the continued use of Group Policy in Entra ID
It combines cloud authentication with on-premises resources and devices
It facilitates seamless transitions and secure access to resources in hybrid environments
It is ideal for organizations that have a mix of cloud and on-premises infrastructure deployments
The following diagram illustrates a device connection to Microsoft Entra ID and the relationship flow for a Microsoft Entra ID hybrid join connection, demonstrating how the connection is made from the device to Microsoft Entra ID as a registration and to an Active Directory for a domain join. Entra ID will then have a hybrid connection to an on-premises Active Directory system, with synchronization occurring between the platforms through the Microsoft Entra Connect service

<img width="1650" height="785" alt="image" src="https://github.com/user-attachments/assets/dd360a8e-c99a-4913-ba3b-86956780c073" />

For more details, refer to https://learn.microsoft.com/en-us/entra/identity/devices/concept-hybrid-join.

Device Settings
Microsoft Entra enables organizations to ensure that their users access Azure resources from devices that comply with their security and compliance policies. Device management is a crucial component of device-based Conditional Access, where access to corporate resources is restricted only to managed devices.

- Users may join devices to Microsoft Entra:
- Users may register their devices with Entra ID
- Require Multi-Factor Authentication to register or join devices with Microsoft Entra
- Maximum number of devices per user
- Manage Additional local administrators on all Microsoft Entra joined devices
- Enable Microsoft Entra Local Administrator Password Solution (LAPS): Local Administrator Password Solution (LAPS)
- Restrict users from recovering the BitLocker key(s) for their owned devices

Enterprise State Roaming
Enterprise State Roaming is a feature in Microsoft Entra ID that allows users to synchronize their application and system settings across their Windows devices. This means that when a user sets up a new Windows device, their familiar settings and preferences will be applied to the new device automaticall





