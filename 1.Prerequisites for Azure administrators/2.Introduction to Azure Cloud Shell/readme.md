# Introduction to Azure Cloud Shell

## What is Azure Cloud Shell?

- Azure Cloud Shell is a command-line environment you can access through your web browser. You can use this environment to manage Azure resources, including VMs, storage, and networking. Just like you do when using the Azure CLI or Azure PowerShell.

- Because Microsoft manages Cloud Shell, you always have access to the most recent versions of the Azure CLI and PowerShell modules right from any browser.

- Azure Cloud Shell also provides cloud storage to persist files such as SSH keys, scripts, and more. This functionality lets you access important files in between sessions and with different machines. Finally, you can use the Cloud Shell editor to make changes to files, such as scripts, that are saved into this cloud storage directly from the Cloud Shell interface.

- Below are sample powershell & bash comands used in azure cloud shell.

```powershell
Get-AzSubscription
```

```console
az account show
```

```bash
code temp.txt
```

## Cloud Shell tools

- If you need to manage resources (such as Docker containers or Kubernetes Clusters) or want to use non-Microsoft tools (such as Ansible and Terraform) in Cloud Shell, the Cloud Shell session comes with these add-ons already preconfigured.

## When should you use Azure Cloud Shell?

> You can use Azure Cloud Shell to:
>
> - Open a secure command-line session from any browser-based device.
> - Interact with Azure resources without the need to install plug-ins or add-ons to your device.
> - Persist files between sessions for later use.
>   \*Use either Bash or PowerShell, whichever you prefer, to manage Azure resources.
> - Edit files (such as scripts) via the Cloud Shell editor.

---

> You shouldn't use Azure Cloud Shell if:
>
> - You intend to leave a session open for more than 20 minutes for long running scripts or activities. In these cases, your session is disconnected without warning, and the current state is lost.
> - You need admin permissions, such as sudo access, from within the Azure CLI or PowerShell environment.
> - You need to install tools that aren't supported in the limited Cloud Shell environment, but instead require an environment such as a custom virtual machine or container.
> - You need storage from different regions. You might need to back up and synchronize this content since only one region can have the storage allocated to Azure Cloud Shell.
> - You need to open multiple sessions at the same time. Azure Cloud Shell allows only one instance at time and isn't suitable for concurrent work across multiple subscriptions or tenants.
