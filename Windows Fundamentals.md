
# Windows Fundamentals

## Windows Fundamentals Part 1

---

### 🪟 Overview of Windows OS
- Windows OS dates back to **1985**
- Dominant OS in **home and corporate environments**
- Frequently targeted by **hackers and malware**
- Current versions:
  - **Windows 11** (Home and Pro)
  - **Windows Server 2025** (server version)

---

### 🖥️ The Desktop (GUI)
- The screen that welcomes you when you log in
- Users can customize desktop appearance and settings

---

### 📁 The File System
- Windows uses **NTFS** (New Technology File System)
- Predecessors: **FAT16**, **FAT32**, and **HPFS**
- **FAT partitions** still used in USBs and microSD cards but not standard for Windows PCs or servers

#### 🔒 NTFS Features:
- **Journaling**: Recovers files after system failure
- **Encryption**
- **File compression**
- **Supports files larger than 4GB**
- **Permission controls** for folders/files

#### NTFS Permission Levels:
- Full control
- Modify
- Read and execute
- List folder contents
- Read
- Write

**To View Permissions:**
1. Right-click the file/folder
2. Select **Properties**
3. Go to the **Security** tab
4. View under **Group or user names**

---

### 🧊 Alternate Data Streams (ADS)
- Feature of NTFS allowing multiple data streams per file
- Hidden from Windows Explorer
- Viewable via **PowerShell** or 3rd-party tools

#### ⚠️ Security Implications:
- Malware may hide data in ADS
- Not always malicious (e.g. internet download identifiers)

---

### 🧬 The `Windows\System32` Folder
- Default OS folder: `C:\Windows` (but doesn’t have to be on C:)
- Accessed using system environment variable: `%windir%`
- Stores critical OS files
- Deleting files in `System32` can render the OS inoperable

---

### 👤 User Accounts, Profiles, and Permissions
- Two main account types:
  - **Administrator**: Full system control
  - **Standard User**: Limited to personal folders/files

**Local User and Group Management:**
- Run `lusrmgr.msc` via Run dialog
- View/manage groups and permissions
- Users can belong to **multiple groups**

---

### 🛡️ User Account Control (UAC)
- Limits the need for elevated privileges
- Reduces risk of malware infection
- Built-in Administrator account **bypasses UAC by default**
- Admin accounts prompt for confirmation when elevation is needed

---

### ⚙️ Settings and Control Panel
- **Settings Menu**: Primary hub for modern system changes
- **Control Panel**: Legacy interface for advanced system configuration

---

### 📊 Task Manager
- Monitors applications and processes running on the system
- Useful for system diagnostics and performance tracking
