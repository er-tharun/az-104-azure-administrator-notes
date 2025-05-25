# Introduction

1. Azure is a cloud platform that provides the compute, storage, and networking resources needed to build cloud-hosted applications.
2. As a new user, the Azure portal is likely to be the primary way you interact with Azure. The Azure portal lets you create and manage all your Azure resources.

## Azure management options

- **Azure portal** for interacting with Azure via a Graphical User Interface (GUI)
- **Azure PowerShell and Azure Command-Line Interface (CLI)** for command-line and automation-based interactions with Azure
- **Azure Cloud Shell** for a web-based command-line interface
- **Azure mobile app** for monitoring and managing your resources from your mobile device

### Azure portal

- The Azure portal is a public website you can access with any web browser. Once you sign in with your Azure account, you can create, manage, and monitor Azure services and resources.

- The Azure portal is often the best interface for carrying out single tasks, or when you want to look at configuration options in detail.

### Azure PowerShell

- Azure PowerShell lets you connect to your Azure subscription and manage resources.

```powershell
New-AzVM -ResourceGroupName "MyResourceGroup" -Name "TestVm" -Image "UbuntuLTS" ...
```

### Azure CLI

- Azure CLI is a command-line program that connects to Azure and executes administrative commands on Azure resources. Azure CLI can run on Windows, Linux, or macOS.

```powershell
az vm create --resource-group MyResourceGroup --name TestVm --image Ubuntu2204 --generate-ssh-keys ...
```

### Azure Cloud Shell

- Azure Cloud Shell is an interactive, authenticated, browser-accessible shell for managing Azure resources using scripting tools like Azure CLI or Azure PowerShell. The Cloud Shell also has many other developer tools available, such as text editors, source-control tools, databases, and more.

### Azure mobile app

- The Microsoft Azure mobile app allows you to access, manage, and monitor all your Azure accounts and resources from your iOS or Android phone or tablet.

### Azure Marketplace

- The Azure Marketplace is often where you start when creating new resources in Azure. The Marketplace lets you find, try, purchase, and provision applications and services from hundreds of leading service providers, all certified to run on Azure.

- The solution catalog spans thousands of offerings across multiple industry categories, such as open-source container platforms, virtual machine images, databases, developer tools, and blockchain. Using Azure Marketplace, you can deploy end-to-end solutions hosted in your own Azure environment.

### Azure Advisor

- Azure Advisor is a free service built into Azure that provides recommendations on high availability, security, performance, operational excellence, and cost. Advisor analyzes your deployed services and suggests ways to improve your environment across those areas. You can view recommendations in the portal or download them in PDF or CSV format.

- You can access Azure Advisor by selecting Advisor from the navigation menu, or search for it in the All Services menu.

### Azure portal dashboards

- A dashboard is a customizable collection of UI tiles displayed in the Azure portal. You can add, remove, and position tiles to create the exact view you want, then save that view as a dashboard. You can configure multiple dashboards, and you can switch among them as needed. You can even share your dashboards with other team members.

- Dashboards give you flexibility in what information to display. For example, you can create dashboards for specific roles within the organization, then use role-based access control (RBAC) to control who can access each dashboard.

- Dashboards are stored as JavaScript Object Notation (JSON) files. This format means you can download a dashboard and edit the file directly, then upload it again to Azure or share it with other users. Azure stores dashboards within resource groups, just like any other resource that you can manage within the portal.

> **Tip:**
> You can also take elements from a resource page and pin them to your dashboard. When using a service, look for the Pin icon. When you select it, you see a Pin to dashboard pane which allows you to select a dashboard (or create a new one) for a tile containing details for that service.

### Clone a dashboard

- Cloning a dashboard creates an instant copy called "Clone of <dashboard name>" and opens that copy in edit mode.

- Cloning is an easy way to create dashboards before sharing them. For example, if you have a dashboard that's similar to a new one you want to share, you can clone it. You can make the changes that you need, and then share it.

### Delete a dashboard

- Deleting a dashboard removes it from your list of available dashboards. You're prompted to confirm that you want to delete the dashboard, but there's no way to recover a deleted dashboard.
- Now, let's try out some of these options by creating a new dashboard.
