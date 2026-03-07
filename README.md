# Enterprise Identity Governance Lab – Microsoft Entra ID

This project demonstrates the implementation of identity governance practices using Microsoft Entra ID.  
The lab simulates an enterprise environment where identities are provisioned, managed, and governed using automated group membership, delegated administration, custom security attributes, and hybrid identity synchronization.

The goal of this project is to demonstrate how identity lifecycle management can be implemented in a modern cloud identity platform.

---

# Project Scenario

Gelo Retail Group is modernizing its identity infrastructure using Microsoft Entra ID while maintaining an on-premises Active Directory environment.

The organization requires:

- Centralized user provisioning
- Automated group membership
- Delegated administration
- Identity classification
- Secure deprovisioning processes
- Hybrid identity synchronization

This project demonstrates how these requirements can be implemented using Microsoft Entra ID.

---

# Architecture Overview

The following diagram illustrates the identity governance flow implemented in this lab.

![Architecture Diagram](Images/P1-Architecture-Diagram.png)

Flow Overview

HR Dataset / CSV  
↓  
User Provisioning (GUI + PowerShell)  
↓  
Group Governance (Assigned + Dynamic Groups)  
↓  
Administrative Units (Delegated Administration)  
↓  
Custom Security Attributes (Identity Classification)  
↓  
User Deprovisioning  
↓  
Hybrid Identity Synchronization


---

# Dataset

The environment uses a sample dataset representing employees across multiple departments.

Departments included:

- Executives
- IT
- HR
- Finance
- Sales

Each user includes attributes used for identity governance:

- Display Name
- Job Title
- Department
- User Principal Name

![User](Images/P1-Users.png)


---

# Identity Provisioning

Users are provisioned using two methods:

- Microsoft Entra Admin Center (GUI)
- Microsoft Graph PowerShell

This demonstrates both manual and automated identity provisioning workflows.

---

## User Provisioning – GUI

Users were provisioned with department attributes to support dynamic group membership and automated access assignment.

![UserProvisioning](Images/User-Provisioining.png)

## Must do before using PowerShell for provisioning
You must do the following first before you start provisioning users using PowerShell:
- Bypass Execution Policy
- Installs the base Microsoft Graph PowerShell module
- Connects to Microsoft Graph

[View Script](Script/MUST-DO-FIRST.txt)

You need to sign in using your Microsoft account

![Microsoftlogin](Images/Connect-to-MgGraph.png)

## User Provisioning – PowerShell

![PowerShellProvisioning](Images/Powershell-Provisioning.png)

[Create individual User](Script/Create-Individual-User.txt)

### Understanding the Script Components

| Component | Explanation | Example |
|-----------|-------------|---------|
| Cmdlet | PowerShell command that follows a Verb-Noun format | `New-MgUser` |
| Parameter | Tells the command how to behave or what data to use | `-DisplayName` |
| String | Text value usually passed to parameters | `"Elon Musk"` |
| Boolean Value | Represents true or false | `$true` |
| Hashtable | Data structure that stores key-value pairs | `@{ Password = "123"; ForceChangePasswordNextSignIn = $true }` |

As per checking in Entra ID, the user was added

![UserAdded](Images/User-Added.png)

## Bulk User Provisioning

Users were provisioned in bulk using both GUI-based CSV upload and PowerShell automation.

### GUI Bulk Creation

Microsoft Entra ID has its own CSV file format, where you can download and input the user information and upload it after the list is created.

![Bulk Upload](Images/Bulk-create-page.png)

You can see the prompt when bulk operations are successful.

![Bulk Upload](Images/Bulk-Operation-successful.png)

### PowerShell Automation

Take note that when we are uploading a csv file using PowerShell, we must use the CSV specifically for PowerShell automation. Not the Microsoft Entra Bulk Template format. You can see sample csv file below:

- [PowerShell Format](Dataset/Bulk-users.csv)
- [Entra Bulk Format](Dataset/UserCreateTemplate.csv)

![PowerShell Bulk Creation](Images/Bulk-create-Powershell.png)





