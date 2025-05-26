# Introduction to PowerShell

## Introduction

- PowerShell is a command-line shell and a scripting language all in one. It was designed as a task engine that uses cmdlets to wrap tasks that people need to do. In PowerShell, you can run commands on local or remote machines. You can do tasks like managing users and automating workflows.

## What is PowerShell?

- PowerShell consists of two parts: a command-line shell and a scripting language. It started out as a framework to automate administrative tasks in Windows. PowerShell has grown into a cross-platform tool that's used for many kinds of tasks.

### Features

    - Built-in help system
    - Pipeline
    - Aliases
    - It operates on objects over text
    - It has cmdlets
    - It has many types of commands

Example powershell commands

```powershell
$PSVersionTable
$PSVersionTable.PSVersion
```

## Locate commands

- A cmdlet (pronounced "command-let") is a compiled command. A cmdlet can be developed in .NET or .NET Core and invoked as a command within PowerShell.
- Cmdlets are named according to a verb-noun naming standard.
- You can see the list of approved verbs by using the **Get-Verb** cmdlet. Verbs are organized according to activity type and function.

Three core cmdlets allow you to delve into what cmdlets exist and what they do:

- **Get-Command:** The Get-Command cmdlet lists all of the available cmdlets on your system. Filter the list to quickly find the command you need.
- **Get-Help:** Run the Get-Help core cmdlet to invoke a built-in help system. You can also run an alias help command to invoke Get-Help but improve the reading experience by paginating the response.
- **Get-Member:** When you call a command, the response is an object that contains many properties. Run the Get-Member core cmdlet to drill down into that response and learn more about it.

### Locate commands by using Get-Command

```powershell
Get-Command -Noun alias*
Get-Command -Verb Get -Noun alias*
```
