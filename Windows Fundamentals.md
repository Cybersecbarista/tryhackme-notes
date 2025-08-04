
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

# Windows Fundamentals 2

---

## System Configuration (`msconfig`)

The System Configuration utility is used for advanced troubleshooting and helps diagnose startup issues. It has five tabs:

- **General**
- **Boot**
- **Services**
- **Startup**
- **Tools**

### General Tab
Choose which devices and services Windows loads at boot:
- Normal
- Diagnostic
- Selective

### Boot Tab
Define boot options for the operating system.

### Services Tab
Lists all services on the system, running or stopped. Services run in the background.

### Startup Tab
MSConfig defers to **Task Manager (`taskmgr`)** for startup item management. It is not a startup management tool itself.

### Tools Tab
Provides quick access to a variety of system utilities for further configuration.

---

## Change UAC Settings

User Account Control (UAC) can be adjusted or disabled (not recommended).

---

## Computer Management (`compmgmt.msc`)

Divided into:
- System Tools
- Storage
- Services and Applications

### System Tools

#### Task Scheduler
Create/manage tasks to run applications or scripts at specific times or triggers.
- Example: run every 5 minutes, at logon, or logoff.

#### Event Viewer
Used to view and audit system events for troubleshooting and monitoring.

Event Viewer panes:
- Left: Hierarchical tree of event log providers.
- Middle: Summary of selected log events.
- Right: Actions pane.

**Event types:**
- Error: Significant issues, e.g., data loss.
- Warning: Possible future problems.
- Information: Successful operations.
- Success Audit: Successful security access.
- Failure Audit: Failed security access.

**Standard Logs:**
- **Application**: App-generated events.
- **Security**: Logon attempts, resource access.
- **System**: System component events.
- **Custom**: App-created logs with custom access control.

---

## Shared Folders

Displays shared folders on the system:
- **Shares**: Lists default shares like `C$`, `ADMIN$`.
- **Sessions**: Users currently connected.
- **Open Files**: Files accessed by connected users.

Right-click a folder > Properties to manage permissions.

---

## Local Users and Groups

Accessible via `lusrmgr.msc` (covered in Windows Fundamentals 1).

---

## Performance Monitor (`perfmon`)

Used for viewing real-time or logged performance data.
Great for troubleshooting local or remote system performance.

---

## Device Manager

Manage and configure attached hardware, including disabling hardware components.

---

## Storage > Disk Management

Tool for managing storage devices:
- Set up new drives
- Extend or shrink partitions
- Assign/change drive letters (e.g., E:)

---

## Services and Applications

### Services
Background applications. You can view, enable/disable, and manage service properties.

### WMI Control
Configures Windows Management Instrumentation (WMI):
> "WMI allows scripting languages (e.g., PowerShell, VBScript) to manage Windows PCs and servers locally/remotely."

**Note**: `WMIC` is deprecated in Windows 10 v21H1. PowerShell supersedes it.

---

## System Information (`msinfo32`)

> "Msinfo32.exe gathers and displays hardware, system, and software environment information."

### Three Sections:
- **Hardware Resources**: Low-level system data (advanced users).
- **Components**: Info about installed hardware (e.g., display, input).
- **Software Environment**: OS-level software data (e.g., environment variables, network connections).

> Example: `WINDIR` stores the location of the Windows directory.

---

## Resource Monitor (`resmon`)

> Displays per-process CPU, memory, disk, and network usage with advanced filtering.

### Resmon Tabs:
- CPU
- Disk
- Network
- Memory

Advanced users can use it for deadlock detection and resolving resource conflicts.

---

## Command Prompt (`cmd`)

A powerful interface for interacting with the system without a GUI.

### Basic Commands:
- `hostname`: Shows the system name.
- `whoami`: Displays the current user.
- `ipconfig`: Displays network address settings.
- `cls`: Clears the terminal screen.

### Help Syntax:
- `command /?` (e.g., `ipconfig /?`) to see options.

### Netstat:
- Displays TCP/IP protocol stats and connections.

### Net Command:
- Manages network resources.
- Help: `net help` or `net help <sub-command>` (e.g., `net help user`)

Sub-commands include:
- `localgroup`
- `use`
- `share`
- `session`

---

## Windows Registry (`regedit`)

> The registry is a central hierarchical database for Windows configuration.

Includes:
- User profiles
- Installed apps
- Hardware configs
- Ports in use

⚠️ Editing the registry can affect system functionality. Use with caution.

**Editor Tool:** `regedit`

