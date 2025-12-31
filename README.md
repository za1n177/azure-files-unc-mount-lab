# Azure Files UNC Mount Lab (AZ-104)

## Overview

This hands-on lab demonstrates how to create and access **Azure File Shares** using **UNC paths over SMB**, including authentication via **storage account keys** and **PowerShell drive mapping**.

The lab validates **real AZ-104 exam scenarios** and bridges traditional on-prem file server concepts with Azure cloud storage.

---

## Skills Demonstrated

- Azure Storage Account configuration  
- Azure Files (SMB) file share creation  
- UNC path construction and usage  
- SMB authentication using storage account keys  
- PowerShell drive mapping (`net use`)  
- File Explorer access to Azure Files  
- Troubleshooting SMB authentication errors (System error 1326)  
- SMB port 445 requirements  

---

## Architecture / Flow

Local Windows Machine
|
| SMB (Port 445)
v
Azure Storage Account
|
v
Azure File Share

yaml
Copy code

**Access methods**
- Windows File Explorer (UNC)
- PowerShell (`net use`)

---

## Step-by-Step Lab

### Step 1 – Create Azure Storage Account

- Create a **Storage Account (GPv2)**
- Enable **Azure Files**
- Note the **storage account name**
- Copy **Access Key 1 or 2**

---

### Step 2 – Create Azure File Share

- Create a file share named `data`
- Access tier: Transaction optimized
- Identity-based access: Not configured

---

### Step 3 – Construct the UNC Path

**Format**
``` **Example** ``` \\stzainisync111.file.core.windows.net\data ``` 

--- 

## Step 4 – Access via File Explorer 

1. Open **File Explorer**
2. Paste the UNC path
3. When prompted:
   - **Username:** `Azure\<storage-account-name>`
   - **Password:** Storage account access key

--- 

## Step 5 – PowerShell Drive Mapping ```powershell net use Z: \\stzainisync111.file.core.windows.net\data /user:Azure\stzainisync111 ``` Verify: ```powershell Get-PSDrive ``` --- ## Screenshots ### SMB Access via File Explorer ![Azure Files SMB Access](screenshots/azure-files-smb-access-file-explorer.png) ### PowerShell Drive Mapping ![Azure Files PowerShell Mount](screenshots/azure-files-powershell-mount.png) 

--- 

## AZ-104 Exam Mapping 

- Manage Azure Storage Accounts
- Configure Azure Files
- Secure storage using UNC paths
- PowerShell automation with `net use`
- Troubleshoot SMB connectivity (port 445, error 1326)

--- 

## Common Errors & Fixes 

### ❌ System error 1326 **Cause:** Incorrect credential format 
**Fix:** 
- Username: `Azure\<storage-account-name>`
- Password: **Storage account access key**

### ❌ Cannot connect to file share 

**Cause:** SMB port 445 blocked 

**Fix:** Allow outbound TCP **445** 

--- 

## Cleanup (Optional) 

```powershell net use Z: /delete ``` 
Delete the file share and storage account if no longer needed. 

--- 

## Key Takeaways 

- Azure Files uses **SMB over port 445**
- UNC paths follow a strict Azure format
- Authentication differs from AD-based file servers
- PowerShell mapping is frequently tested in AZ-104
- Hands-on troubleshooting improves exam success
