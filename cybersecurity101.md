# Search Skills - TryHackMe Notes

## Introduction

We are surrounded by information. Do you prefer to surrender in the face of information overload and accept the first few results you get? Or do you like to acquire the necessary search skills to find and access what you are looking for? This room aims to help you with the latter.

---

## Learning Objectives

The goal of this room is to teach:

- Evaluate information sources  
- Use search engines efficiently  
- Explore specialized search engines  
- Read technical documentation  
- Make use of social media  
- Check news outlets  

---

## Evaluation of Search Results

On the Internet, everyone can publish their writings. It can be in the form of blog posts, articles, or social media posts. It can be even in more subtle ways, such as by editing a public wiki page. This ability makes it possible for anyone to voice their unfounded claims. Everyone can express their opinion about best cyber security practices, future programming trends, and how to best prepare for a DevSecOps interview.

It is our job, as readers, to evaluate the information. Here are a few things to consider:

- **Source**: Identify the author or organization. Are they reputable?
- **Evidence and reasoning**: Are claims backed by credible evidence?
- **Objectivity and bias**: Is the information presented impartially?
- **Corroboration and consistency**: Can you find agreement from multiple sources?

---

## Search Engines

Most people use search engines, but few use them efficiently. Consider the following search engines:

- Google  
- Bing  
- DuckDuckGo  

### Common Search Operators (Google)

- `"exact phrase"` – Finds exact matches  
- `site:` – Restricts results to a specific domain (e.g., `site:tryhackme.com`)  
- `-` – Excludes a term (e.g., `pyramids -tourism`)  
- `filetype:` – Finds specific file types (e.g., `filetype:ppt cyber security`)  

---

## Specialized Search Engines

### Shodan

Search engine for devices connected to the Internet (e.g. Apache 2.4.1 servers).

### Censys

Focuses on Internet hosts, websites, certificates. Useful for:

- Enumerating domains  
- Auditing ports/services  
- Discovering rogue assets  

### VirusTotal

Scans files/URLs with multiple antivirus engines. Also supports hash lookup.

### Have I Been Pwned (HIBP)

Checks if your email has appeared in data breaches.

---

## Vulnerabilities and Exploits

### CVE

The CVE program provides a standard ID for vulnerabilities (e.g., CVE-2024-29988). Managed by MITRE.  
See: [CVE Website](https://cve.mitre.org) and [NVD](https://nvd.nist.gov)

### Exploit Database

Hosts verified and unverified exploits for security testing (with permission only).  
GitHub is also a rich source of PoCs and tools.

---

## Technical Documentation

### Linux Manual Pages

Use `man <command>` for official command documentation.

### Microsoft Docs

Microsoft provides technical documentation for its platforms.

### Product Docs

Always refer to official docs (e.g., Snort, Apache, PHP, Node.js) for:

- Latest updates  
- Full feature descriptions  

---

## Social Media and News

Social media is useful for:

- Tracking cybersecurity trends  
- Monitoring employee oversharing risks  
- Discovering vulnerabilities in real-time  

Follow cyber-focused channels and news outlets to stay updated.


# 🧠 Active Directory Basics

## 🏢 Introduction to Active Directory
Microsoft's Active Directory is the backbone of the corporate world. It simplifies the management of devices and users within a corporate environment.

### 🌐 Windows Domains
A Windows domain is a group of users and computers under centralized administration. The Domain Controller (DC) is the server that runs Active Directory services.

### ✅ Benefits
- Centralized identity management
- Manageable security policies

## 🧪 Real-World Example
In schools or offices, user credentials are validated across machines by the domain controller, which applies policies and restrictions centrally.

## 🧩 Active Directory Domain Services (AD DS)
Acts as a catalog for all network "objects":
- Users
- Machines
- Security groups
- Printers, etc.

### 👤 Users
- Represent people or services
- Can be authenticated and granted permissions
- Services like IIS/MSSQL use service accounts

### 💻 Machines
- Join the domain as objects (security principals)
- Named like `DC01$`
- Passwords rotated and long

### 🛡️ Security Groups
- Assign permissions to users/machines
- Nested groups allowed
- Common Groups:
  - Domain Admins
  - Server Operators
  - Backup Operators
  - Account Operators
  - Domain Users, Computers, Controllers

## 🗂️ Active Directory Users and Computers (ADUC)
Tool used to manage users/groups/machines in OUs:
- OUs mimic business structure
- Each user can belong to only one OU
- Containers:
  - Builtin
  - Computers
  - Domain Controllers
  - Users
  - Managed Service Accounts

## 📌 OUs vs Security Groups
| Organizational Units (OUs) | Security Groups |
|----------------------------|------------------|
| Used for policy application | Used for permission management |
| Only one OU per user        | Users can be in multiple groups |

## 🧑‍💻 Managing Users in AD

### 🔁 Delegation
Delegation allows giving specific privileges to users (like Helpdesk) to manage OUs without being Domain Admins.

## 🖥️ Managing Computers in AD
Default location: "Computers" container  
Best practice: Separate by function:
- Workstations (daily use, no elevated access)
- Servers (host services)
- Domain Controllers (most sensitive)

## ⚙️ Group Policies
GPOs let you apply settings to users/computers in an OU.

### 🛠️ Creating GPOs
1. Use Group Policy Management Tool
2. Create GPO under "Group Policy Objects"
3. Link GPO to target OU

### 🧰 Settings and Security Filtering
- GPOs apply to linked OU and sub-OUs
- Can restrict with Security Filtering (e.g., apply only to a group)

### 🔁 Distribution via SYSVOL
GPOs are distributed via:
```
\<domain>\SYSVOL
```

### 🕐 GPO Sync
- Syncs every 90–120 minutes
- Force sync with:
```bash
gpupdate /force
```

## 🔐 Authentication Methods

### Kerberos (Default)
- Uses tickets (TGT, TGS)
- Key Distribution Center (KDC) runs on Domain Controller
- Secure and efficient

### NetNTLM (Legacy)
- Challenge-response method
- Still used for compatibility
- Password hash never transmitted

## 🌳 Trees, Forests, Trusts

### Trees
- Domains in the same namespace
- Example: `uk.thm.local`, `us.thm.local` under `thm.local`

### Forests
- Domains with different namespaces
- Example: `thm.local` and `mht.local`

### Trust Relationships
- Allow cross-domain access
- One-way or two-way
- Trust ≠ access; permissions still need to be granted

---

## Conclusion

As the information landscape evolves, staying plugged into the right channels and resources helps you stay sharp and ahead of the curve.

# Windows Command Line Notes

> Everyone prefers a graphical user interface (GUI) until they master a command-line interface (CLI). There are many reasons for that.

GUIs are usually intuitive—you can explore and figure them out quickly. CLIs often have a learning curve, but once mastered, they can be faster and more efficient.

Example: Checking your IP address  
- GUI: Multiple clicks through menus.  
- CLI: Type one command, no mouse needed.

## Advantages of CLI
- **Lower resource usage**: Runs on older hardware or limited memory systems. Saves resources in cloud computing.
- **Automation**: Easy to script tasks with batch files.
- **Remote management**: Use SSH for servers, routers, IoT devices, even on slow networks.

---

## Basic System Information

**Commands:**

```cmd
set
```
Displays environment variables including the system `Path`.

```cmd
ver
```
Shows the Windows OS version.

```cmd
systeminfo
```
Displays detailed system information (OS, processor, memory, etc.).  
Use `| more` to view page-by-page.

```cmd
driverquery
driverquery | more
```
Lists drivers (page-by-page with `| more`).

```cmd
help
```
Help information for a command.

```cmd
cls
```
Clears the Command Prompt screen.

---

## Network Troubleshooting

**Network Configuration:**

```cmd
ipconfig
ipconfig /all
```
View basic or detailed network configuration.

**Connectivity Tests:**

```cmd
ping target_name
```
Check if a target is reachable.

```cmd
tracert target_name
```
Trace route to target.

**DNS Lookup:**

```cmd
nslookup example.com
nslookup example.com 1.1.1.1
```
Look up domain info (optional specific DNS server).

**Network Statistics:**

```cmd
netstat
netstat -abon
```
- `-a`: all connections/listening ports  
- `-b`: program using the port  
- `-o`: process ID  
- `-n`: numeric format

---

## File and Disk Management

**Directories:**

```cmd
cd
```
Show current directory.

```cmd
dir
dir /a
dir /s
```
List directory contents (`/a` for hidden, `/s` for subdirectories).

```cmd
tree
```
Graph view of directories.

```cmd
cd target_directory
cd ..
```
Navigate into or up directories.

```cmd
mkdir directory_name
rmdir directory_name
```
Create or remove directories.

**Files:**

```cmd
type file.txt
more file.txt
```
View text files (`more` for paging).

```cmd
copy source destination
move source destination
```
Copy or move files.

```cmd
del file.txt
erase file.txt
```
Delete files (`*` wildcard for multiple).

---

## Tasks and Process Management

```cmd
tasklist
```
List running processes.

```cmd
tasklist /FI "imagename eq sshd.exe"
```
Filter processes by name.

```cmd
taskkill /PID 4567
```
Kill process by PID.

---
# Windows PowerShell

## What is PowerShell?
From the official Microsoft page: “PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework.”

PowerShell is a powerful tool from Microsoft designed for task automation and configuration management. It combines a command-line interface and a scripting language built on the .NET framework. Unlike older text-based command-line tools, PowerShell is object-oriented, which means it can handle complex data types and interact with system components more effectively. Initially exclusive to Windows, PowerShell has lately expanded to support macOS and Linux, making it a versatile option for IT professionals across different operating systems.

## A Brief History of PowerShell
PowerShell was developed to overcome the limitations of existing command-line tools and scripting environments in Windows. In the early 2000s, as Windows was increasingly used in complex enterprise environments, traditional tools like cmd.exe and batch files fell short in automating and managing these systems. Microsoft needed a tool that could handle more sophisticated administrative tasks and interact with Windows’ modern APIs.

Jeffrey Snover, a Microsoft engineer, realised that Windows and Unix handled system operations differently—Windows used structured data and APIs, while Unix treated everything as text files. This difference made porting Unix tools to Windows impractical. Snover’s solution was to develop an object-oriented approach, combining scripting simplicity with the power of the .NET framework. Released in 2006, PowerShell allowed administrators to automate tasks more effectively by manipulating objects, offering deeper integration with Windows systems.

As IT environments evolved to include various operating systems, the need for a versatile automation tool grew. In 2016, Microsoft responded by releasing PowerShell Core, an open-source and cross-platform version that runs on Windows, macOS, and Linux.

## The Power in PowerShell
To fully grasp the power of PowerShell, we first need to understand what an object is in this context.

In programming, an object represents an item with properties (characteristics) and methods (actions). For example, a car object might have properties like `Color`, `Model`, and `FuelLevel`, and methods like `Drive()`, `HonkHorn()`, and `Refuel()`.

Similarly, in PowerShell, objects are fundamental units that encapsulate data and functionality, making it easier to manage and manipulate information. An object in PowerShell can contain file names, usernames or sizes as data (properties), and carry functions (methods) such as copying a file or stopping a process.

The traditional Command Shell’s basic commands are text-based, meaning they process and output data as plain text. Instead, when a cmdlet (pronounced command-let) is run in PowerShell, it returns objects that retain their properties and methods. This allows for more powerful and flexible data manipulation since these objects do not require additional parsing of text.

## PowerShell Basics

### Basic Syntax: Verb-Noun
PowerShell commands are known as **cmdlets**. They follow a `Verb-Noun` naming convention:

- **Verb**: Describes the action.
- **Noun**: Specifies the object of the action.

Examples:
- `Get-Content`: Retrieves the content of a file.
- `Set-Location`: Changes the current working directory.

### Basic Cmdlets
- `Get-Command`: Lists all available cmdlets, functions, aliases, and scripts.
- `Get-Help`: Provides detailed information about cmdlets, including usage and examples.
- `Get-Alias`: Lists all aliases (shortcuts) for cmdlets.

### Finding and Installing Cmdlets
- `Find-Module`: Searches online repositories like PowerShell Gallery.
- `Install-Module`: Installs a module from an online repository.

## Navigating the File System and Working with Files
- `Get-ChildItem`: Lists files and directories.
- `Set-Location`: Changes the current directory.
- `New-Item`: Creates a new file or directory.
- `Remove-Item`: Deletes a file or directory.
- `Copy-Item`: Copies a file or directory.
- `Move-Item`: Moves a file or directory.
- `Get-Content`: Displays the contents of a file.

## Piping, Filtering, and Sorting Data
- Piping (`|`) passes **objects** from one cmdlet to another.
- `Sort-Object`: Sorts objects by a property.
- `Where-Object`: Filters objects based on conditions.
- Comparison operators:
  - `-eq`: Equal to
  - `-ne`: Not equal to
  - `-gt`: Greater than
  - `-ge`: Greater than or equal to
  - `-lt`: Less than
  - `-le`: Less than or equal to
- `Select-Object`: Selects specific object properties or limits output.
- `Select-String`: Searches for text patterns in files (supports regex).

## System and Network Information
- `Get-ComputerInfo`: Retrieves comprehensive system information.
- `Get-LocalUser`: Lists local user accounts.
- `Get-NetIPConfiguration`: Displays network interface details.
- `Get-NetIPAddress`: Shows configured IP addresses.

## Real-Time System Analysis
- `Get-Process`: Lists running processes.
- `Get-Service`: Displays service statuses.
- `Get-NetTCPConnection`: Shows active TCP connections.
- `Get-FileHash`: Generates file hashes.

## Scripting in PowerShell
- Scripts automate repetitive tasks and can be defensive or offensive in cybersecurity.
- Blue team use cases: Log analysis, detecting anomalies, automating scans.
- Red team use cases: Enumeration, remote command execution, obfuscation.
- `Invoke-Command`: Executes commands on remote systems.

A shell script is nothing but a set of commands. Suppose a repetitive task requires you to enter multiple commands using a shell. Instead of entering them one after one on every repetition of that task, which may take more of your time, you can combine them into a script. To execute all those commands, you will only execute the script, and all the commands will be executed. All the shells mentioned in the previous tasks have scripting capabilities. Scripting helps us to automate tasks. Before learning how to write a script, we need to know that even though Linux shells have scripting capabilities, this does not mean that you can only make a script using a shell. Scripting can be done in various programming languages as well. However, the scope of this room is to cover scripting using a shell.

The first step is to open the terminal and select a shell. Let’s go with the bash shell, the default, and widely used shell in most distributions.

Unlike the other commands we type in the shell, we first need to create a file using any text editor for the script. The file must be named with an extension .sh, the default extension for bash scripts. The following terminal shows the script file creation:

Create Script File
user@tryhackme:~$ nano first_script.sh
Every script should start from shebang. Shebang is a combination of some characters that are added at the beginning of a script, starting with #! followed by the name of the interpreter to use while executing the script. As we are writing our script in bash, let’s define it as the interpreter in the shebang.

first_script.sh
#!/bin/bash
We are all set to write our first script now. There are some fundamental building blocks of a script that together make an efficient script. Let’s learn and utilize these script constructs to write one script ourselves.

Variables

A variable stores a value inside it. Suppose you need to use some complex values, like a URL, a file path, etc., several times in your script. Instead of memorizing and writing them repeatedly, you can store them in a variable and use the variable name wherever you need it.

The script below displays a string on the screen: "Hey, what’s your name?” This is done by echo command. The second line of the script contains the code read name. read is used to take input from the user, and name is the variable in which the input would be stored. The last line uses echo to display the welcome line for the user, along with its name stored in the variable.

# Defining the Interpreter 
#!/bin/bash
echo "Hey, what’s your name?"
read name
echo "Welcome, $name"
Now, save the script by pressing CTRL+X. Confirm by pressing Y and then ENTER.
To execute the script, we first need to make sure that the script has execution permissions. To give these permissions to the script, we can type the following command in our terminal:

Execution Permission to Script
user@tryhackme:~$ chmod +x first_script.sh
Now that the script has execution permissions use ./ before the script name to execute it. We use ./ before the script to run rather than typing the script name directly because ./ tells the shell to execute the file that is present in the current directory. If you don't define ./ before the script name, the shell will search the script in the PATH environment variable (that contains all the directories except the current one), and it will not find the defined script in any of those directories and generate an error. The below terminal shows the script in which we utilized the variables:

Script Execution
user@ubuntu:~$ ./first_script.sh
Hey, What's your name?
John
Welcome, John
Loops
Loop, as the name suggests, is something that is repeating. For example, you have a list of many friends, and you want to send them the same message. Instead of sending them individually, you can make a loop in your script, give your friend list to the loop and the message, and it will send that message to all your friends.

For a general explanation of loops, let’s write a loop that will display all numbers starting from 1 to 10 on the screen. First, create a new file named loop_script.sh, then enter the code below. Save your file by pressing CRTL+X, then confirm with y and then ENTER.

# Defining the Interpreter 
#!/bin/bash
for i in {1..10};
do
echo $i
done
The first line has the variable i that will iterate from 1 to 10 and execute the below code every time. do indicates the start of the loop code, and done indicates the end. In between them, the code we want to execute in the loop is to be written. The for loop will take each number in the brackets and assign it to the variable i in each iteration. The echo $i will display this variable’s value every iteration.

Now, let’s execute the script after giving it the execution permission.

Script Execution
user@tryhackme:~$ ./loop_script.sh
1
2
3
The output of the above terminal is cut to 3 numbers only for demonstration. However, when executed according to the script's logic, it would display the numbers from 1 to 10.

Conditional Statements

Conditional statements are an essential part of scripting. They help you execute a specific code only when a condition is satisfied; otherwise, you can execute another code. Suppose you want to make a script that shows the user a secret. However, you want it to be shown to only some users, only to the high-authority user. You will create a conditional statement that will first ask the user their name, and if that name matches the high authority user’s name, it will display the secret. 

First, create a new file named conditional_script.sh, then enter the code below. Save your file by pressing CRTL+X, then confirm with y and then ENTER.

# Defining the Interpreter 
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi
The above script takes the user’s name as input and stores it into a variable (studied in the Variables section). The conditional statement starts with if and compares the value of that variable with the string Stewart; if it’s a match, it will display the secret to the user, or else it will not. The fi is used to end the condition.

Following is the terminal showing the script execution when the user name matches the authorized one defined in the script:

conditional_script.sh
user@tryhackme:~$ ./conditional_script.sh
Please enter your name first:
Stewart
Welcome, Stewart! Here is the secret: THM_Script
However, the following terminal shows the script execution when the user name does not match the authorized one defined in the script:

conditional_script.sh
user@tryhackme:~$ ./conditional_script.sh
Please enter your name first:
Alex
Sorry! You are not authorized to access the secret.
Comments

Sometimes, the code can be very lengthy. In this scenario, the code might confuse you when you look at it after some time or share it with somebody. An easy way to resolve this problem is to use comments in different parts of the code. A comment is a sentence that we write in our code just for the sake of our understanding. It is written with a # sign followed by a space and the sentence you need to write. For example, let’s rewrite the script we discussed in the conditional statements section and add comments to it. Open the conditional_script.sh with nano, then add the comments starting with a # sign. Save your file by pressing CRTL+X, then confirm with y and then ENTER.

# Defining the Interpreter
#!/bin/bash

# Asking the user to enter a value.
echo "Please enter your name first:"

# Storing the user input value in a variable.
read name

# Checking if the name the user entered is equal to our required name.
if [ "$name" = "Stewart" ]; then

# If it equals the required name, the following line will be displayed.
echo "Welcome Stewart! Here is the secret: THM_Script"

# Defining the sentence to be displayed if the condition fails.
else
        echo "Sorry! You are not authorized to access the secret."
fi
See how easy a script looks with comments. Comments don’t affect the working of any script. A good script always has some comments. The example shown above contains a comment for each line. This is just a better explanation of its concept. However, the best way to include comments is to define them in the major and complex areas of the script.

Note: Other types of variables, loops, and conditional statements can also be used to achieve different tasks. Moreover, multiple lines of comments can also be added within a single comment. However, it is not the scope of this room.
