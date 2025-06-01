# Introduction

- Microsoft Entra ID is a cloud-based identity and access management service provided by Microsoft. Microsoft Entra ID is a comprehensive solution for managing identities, enforcing access policies, and securing your applications and data in the cloud and on-premises.

## Examine Microsoft Entra ID

- AD DS is a directory service that provides the methods for storing directory data, such as user accounts and passwords, and makes this data available to network users, administrators, and other devices and services. It runs as a service on Windows Server, referred to as a domain controller.
- Microsoft Entra ID is part of the platform as a service (PaaS) offering and operates as a Microsoft-managed directory service in the cloud. It’s not a part of the core infrastructure that customers own and manage, nor is it an Infrastructure as a service offering. While this implies that you have less control over its implementation, it also means that you don’t have to dedicate resources to its deployment or maintenance.

- With Microsoft Entra ID, you also have access to a set of features that aren’t natively available in AD DS, such as support for multi-factor authentication, identity protection, and self-service password reset.
- You can use Microsoft Entra ID to provide more secure access to cloud-based resources for organizations and individuals by:

  - Configuring access to applications
  - Configuring single sign-on (SSO) to cloud-based SaaS applications
  - Managing users and groups
  - Provisioning users
  - Enabling federation between organizations
  - Providing an identity management solution
  - Identifying irregular sign-in activity
  - Configuring multi-factor authentication
  - Extending existing on-premises Active Directory implementations to Microsoft Entra ID
  - Configuring Application Proxy for cloud and local applications
  - Configuring Conditional Access for users and devices

> **NOTE:** By default, when you create a new Azure subscription by using a Microsoft account, the subscription automatically includes a new Microsoft Entra tenant named Default Directory.

## Microsoft Entra tenants

- Unlike AD DS, Microsoft Entra ID is multi-tenant by design and is implemented specifically to ensure isolation between its individual directory instances. It’s the world’s largest multi-tenant directory, hosting over a million directory services instances, with billions of authentication requests per week.
- The term tenant in this context typically represents a company or organization that signed up for a subscription to a Microsoft cloud-based service such as Microsoft 365, Intune, or Azure, each of which uses Microsoft Entra ID.
- However, from a technical standpoint, the term tenant represents an individual Microsoft Entra instance. Within an Azure subscription, you can create multiple Microsoft Entra tenants. Having multiple Microsoft Entra tenants might be convenient if you want to test Microsoft Entra functionality in one tenant without affecting the others.
- At any given time, an Azure subscription must be associated with one, and only one, Microsoft Entra tenant. This association allows you to grant permissions to resources in the Azure subscription (via RBAC) to users, groups, and applications that exist in that particular Microsoft Entra tenant.

> **NOTE:** At any given time, an Azure subscription must be associated with one, and only one, Microsoft Entra tenant. This association allows you to grant permissions to resources in the Azure subscription (via RBAC) to users, groups, and applications that exist in that particular Microsoft Entra tenant.

- Each Microsoft Entra tenant is assigned the default Domain Name System (DNS) domain name, consisting of a unique prefix. The prefix, derived from the name of the Microsoft account you use to create an Azure subscription or provided explicitly when creating a Microsoft Entra tenant, is followed by the onmicrosoft.com suffix.
- Adding at least one custom domain name to the same Microsoft Entra tenant is possible and common. This name utilizes the DNS domain namespace that the corresponding company or organization owns.
- The Microsoft Entra tenant serves as the security boundary and a container for Microsoft Entra objects such as users, groups, and applications. A single Microsoft Entra tenant can support multiple Azure subscriptions.

## Microsoft Entra schema

- The Microsoft Entra schema contains fewer object types than that of AD DS. Most notably, it doesn't include a definition of the computer class, although it does include the device class.

- The process of joining devices to Microsoft Entra differs considerably from the process of joining computers to AD DS. The Microsoft Entra schema is also easily extensible, and its extensions are fully reversible.
- The lack of support for the traditional computer domain membership means that you can't use Microsoft Entra ID to manage computers or user settings by using traditional management techniques, such as Group Policy Objects (GPOs). Instead, Microsoft Entra ID and its services define a concept of modern management. Microsoft Entra ID’s primary strength lies in providing directory services; storing and publishing user, device, and application data; and handling the authentication and authorization of the users, devices, and applications. The effectiveness and efficiency of these features are apparent based on existing deployments of cloud services such as Microsoft 365, which rely on Microsoft Entra ID as their identity provider and support millions of users.
- Microsoft Entra ID doesn't include the organizational unit (OU) class, which means that you can't arrange its objects into a hierarchy of custom containers, which is frequently used in on-premises AD DS deployments. However, this isn't a significant shortcoming, because OUs in AD DS are used primarily for Group Policy scoping and delegation. You can accomplish equivalent arrangements by organizing objects based on their group membership.
- Objects of the Application and servicePrincipal classes represent applications in Microsoft Entra ID. An object in the Application class contains an application definition and an object in the servicePrincipal class constitutes its instance in the current Microsoft Entra tenant. Separating these two sets of characteristics allows you to define an application in one tenant and use it across multiple tenants by creating a service principal object for this application in each tenant. Microsoft Entra ID creates the service principal object when you register the corresponding application in that Microsoft Entra tenant.

## Compare Microsoft Entra ID and Active Directory Domain Services.

### Characteristics of AD DS

- AD DS is the traditional deployment of Windows Server-based Active Directory on a physical or virtual server.
- Although AD DS is commonly considered being primarily a directory service, it’s only one component of the Windows Active Directory suite of technologies, which also includes
  - Active Directory Certificate Services (AD CS),
  - Active Directory Lightweight Directory Services (AD LDS), - Active Directory Federation Services (AD FS), and
  - Active Directory Rights Management Services (AD RMS).
- When comparing AD DS with Microsoft Entra ID, it’s important to note the following characteristics of AD DS:
  - AD DS is a true directory service, with a hierarchical X.500-based structure.
  - AD DS uses Domain Name System (DNS) for locating resources such as domain controllers.
  - You can query and manage AD DS by using Lightweight Directory Access Protocol (LDAP) calls.
  - AD DS primarily uses the Kerberos protocol for authentication.
  - AD DS uses OUs and GPOs for management.
  - AD DS includes computer objects, representing computers that join an Active Directory domain.
  - AD DS uses trusts between domains for delegated management.
- You can deploy AD DS on an Azure virtual machine to enable scalability and availability for an on-premises AD DS. However, deploying AD DS on an Azure virtual machine doesn't make any use of Microsoft Entra ID.

> **NOTE:** Deploying AD DS on an Azure virtual machine requires one or more extra Azure data disks because you shouldn't use drive C for AD DS storage. These disks are needed to store the AD DS database, logs, and the sysvol folder. The Host Cache Preference setting for these disks must be set to None.

### Characteristics of Microsoft Entra ID

When comparing Microsoft Entra ID with AD DS, it’s important to note the following characteristics of Microsoft Entra ID:

- Microsoft Entra ID is primarily an identity solution, and it’s designed for internet-based applications by using HTTP (port 80) and HTTPS (port 443) communications.
- Microsoft Entra ID is a multi-tenant directory service.
  Microsoft Entra users and groups are created in a flat structure, and there are no OUs or GPOs.
- You can't query Microsoft Entra ID by using LDAP; instead, Microsoft Entra ID uses the REST API over HTTP and HTTPS.
- Microsoft Entra ID doesn't use Kerberos authentication instead, it uses HTTP and HTTPS protocols such as SAML, WS-Federation, and OpenID Connect for authentication, and uses OAuth for authorization.
- Microsoft Entra ID includes federation services, and many third-party services such as Facebook are federated with and trust Microsoft Entra ID.

## Examine Microsoft Entra ID as a directory service for cloud apps

- It’s now possible to have one identity service that covers all Microsoft cloud-based services, such as Microsoft 365, Azure, Microsoft Dynamics 365, and Intune. Microsoft Entra ID provides developers with centralized authentication and authorization for applications in Azure by using other identity providers or on-premises AD DS. Microsoft Entra ID can provide users with an SSO experience when using applications such as Facebook, Google services, Yahoo, or Microsoft cloud services.
- In particular, you can enable Microsoft Entra authentication for the Web Apps feature of Azure App Service directly from the Authentication/Authorization blade in the Azure portal. By designating the Microsoft Entra tenant, you can ensure that only users with accounts in that directory can access the website. It’s possible to apply different authentication settings to individual deployment slots.

## Compare Microsoft Entra ID P1 and P2 plans

### Microsoft Entra ID P1 edition

- Self-service group management.
- Advanced security reports and alerts.
- Multi-factor authentication.
- **Microsoft Identity Manager (MIM) licensing.** MIM integrates with Microsoft Entra ID P1 or P2 to provide hybrid identity solutions. MIM can bridge multiple on-premises authentication stores such as AD DS, LDAP, Oracle, and other applications with Microsoft Entra ID. This provides consistent experiences to on-premises line-of-business (LOB) applications and SaaS solutions.
- Enterprise SLA of 99.9%.
- Password reset with writeback.
- Cloud App Discovery feature of Microsoft Entra ID.
- Conditional Access based on device, group, or location.
- Microsoft Entra Connect Health.

### Microsoft Entra ID P2 license

- **Microsoft Entra ID Protection.** provides enhanced functionalities for monitoring and protecting user accounts. You can define user risk policies and sign-in policies. In addition, you can review users’ behavior and flag users for risk.
- **Microsoft Entra Privileged Identity Management.** This functionality lets you configure additional security levels for privileged users such as administrators. With Privileged Identity Management, you define permanent and temporary administrators. You also define a policy workflow that activates whenever someone wants to use administrative privileges to perform some task.

## Examine Microsoft Entra Domain Services

- In most organizations today, line-of-business (LOB) applications are deployed on computers and devices that are domain members. These organizations use AD DS–based credentials for authentication, and Group Policy manages them. When you consider moving these apps to run in Azure, one key issue is how to provide authentication services to these apps. To satisfy this need, you can choose to implement a site-to-site virtual private network (VPN) between your local infrastructure and the Azure IaaS, or you can deploy replica domain controllers from your local AD DS as virtual machines (VMs) in Azure. These approaches can entail additional costs and administrative effort. Additionally, the difference between these two approaches is that with the first option, authentication traffic will cross the VPN, while in the second option, replication traffic will cross the VPN and authentication traffic stays in the cloud.

- Microsoft provides Microsoft Entra Domain Services as an alternative to these approaches. This service, which runs as part of the Microsoft Entra ID P1 or P2 tier, provides domain services such as Group Policy management, domain joining, and Kerberos authentication to your Microsoft Entra tenant. These services are fully compatible with locally deployed AD DS, so you can use them without deploying and managing additional domain controllers in the cloud.

  ![alt text](https://learn.microsoft.com/en-us/training/wwl-azure/understand-azure-active-directory/media/azure-active-directory-virtual-network-340081c4.png)

Microsoft Entra Domain Services provides several benefits for organizations, such as:

- Administrators don't need to manage, update, and monitor domain controllers.
- Administrators don't need to deploy and manage Active Directory replication.
- There’s no need to have Domain Admins or Enterprise Admins groups for domains that Microsoft Entra ID manages.

If you choose to implement Microsoft Entra Domain Services, you need to be aware of the service's current limitations. These include:

- Only the base computer Active Directory object is supported.
- It’s not possible to extend the schema for the Microsoft Entra Domain Services domain.
- The organizational unit (OU) structure is flat and nested OUs aren't currently supported.
- There’s a built-in Group Policy Object (GPO), and it exists for computer and user accounts.
- It’s not possible to target OUs with built-in GPOs. Additionally, you can't use Windows Management Instrumentation filters or security-group filtering.

By using Microsoft Entra Domain Services, you can freely migrate applications that use LDAP, NTLM, or the Kerberos protocols from your on-premises infrastructure to the cloud. You can also use applications such as Microsoft SQL Server or Microsoft SharePoint Server on VMs or deploy them in the Azure IaaS, without needing domain controllers in the cloud or a VPN to local infrastructure.

You can enable Microsoft Entra Domain Services by using the Azure portal. This service charges per hour based on the size of your directory.
