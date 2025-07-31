# Linux Fundamentals Part 1 🐧

## Overview
Linux is a very popular operating system, widely used due to its lightweight and flexible nature.  
You'll find it running in:

- Game consoles  
- Android devices  
- Smart cars  
- Websites  
- Point of Sale (POS) systems  
- Traffic light controllers  

---

## Background on Linux
- Linux is **lightweight** and **open source**
- Based on the **UNIX** operating system
- Offers a wide range of **distributions** ("distros")

Popular distributions include:
- **Ubuntu**
- **Debian**

These are widely used because of their flexibility and support for server configurations.

---

## Using the Terminal

### Why the Terminal?
- Many Linux systems (like Ubuntu Server) run **without a GUI (Graphical User Interface)**
- Most interactions are done through the **Terminal**

---

## Basic Commands

- `echo` – Output any text we provide  
- `whoami` – Find out what user we're logged in as  
- `ls` – List files and directories in the current location  
- `cd` – Change directory  
- `ctrl + L` – Clears the terminal screen  
- `cat` – Output the contents of a file (concatenate)  
- `pwd` – Print working directory  

---

## Searching for Files

### `find`
- Used to locate files when you **know the file name** or want to match a pattern  
- Can search all directories under the current location  

Examples:
- `find -name "filename.txt"`  
- `find -name "*.txt"`

---

## Using `grep`

- `grep` allows you to **search the contents of files** for specific keywords or values  

Examples:
- `grep "keyword" filename.txt`  
- `cat file.txt | grep "search_term"`

---

## Shell Operators

- `&` – Runs a command in the background of your terminal (e.g., copying a large file)  
- `&&` – Combines multiple commands together in one line; second command runs only if the first succeeds  
- `>` – Redirects the output from a command and **overwrites** contents of a file if it already exists  
- `>>` – Redirects output like `>` but **appends** it to the end of a file rather than overwriting

Examples:
- `echo "hello" > file.txt` – Overwrites `file.txt` with `hello`  
- `echo "world" >> file.txt` – Appends `world` to the end of `file.txt`

---
# Linux Fundamentals Part 2

## SSH (Secure Shell)
- SSH is a protocol that enables secure, encrypted communication between devices.
- It allows you to remotely execute commands on another device.
- All transmitted data is encrypted over the network.

### Using SSH to Login to a Linux Machine
To connect to a remote machine, you need:
1. The IP address of the remote machine
2. Valid credentials to log into an account on that machine

**Command Syntax:**
```bash
ssh username@ip_address
```
**Example:**
```bash
ssh tryhackme@10.10.25.210
```

---

## Flags and Switches
- Most commands accept **arguments** called **flags** or **switches**, identified by a hyphen (`-`).
- These modify or extend the behavior of commands.

**Examples:**
- `-a`: Shows all files and folders (including hidden ones).
- `--help`: Lists all possible options for the command with descriptions.

---

## The Man (Manual) Page
- Provides documentation for system commands and applications.
- Can be accessed directly from the terminal.

**Example:**
```bash
man ls
```
(Displays the manual for the `ls` command)

---

## Filesystem Interaction (Continued)

### `touch`
- Creates a blank file.
```bash
touch note
```
> Use `echo` or a text editor like `nano` to add content.

### `mkdir`
- Makes a directory (folder).
```bash
mkdir mydirectory
```

### `rm`
- Removes a file or directory.
- Use `-R` to recursively remove directories.
```bash
rm -R mydirectory
```

### `cp`
- Copies a file or folder.
```bash
cp original.txt copy.txt
```
> Copies content of `original.txt` into `copy.txt`

### `mv`
- Moves or renames a file or folder.
```bash
mv note2 note3
```
> `note3` will now have the contents of `note2`

### `file`
- Determines the type of a file.
```bash
file myfile
```

---

## Permissions 101
- The first three columns in a directory listing show file permissions.
- Permissions are defined by **Read**, **Write**, and **Execute**.

### Ownership
- A file can be owned by a user and/or a group.
- Permissions can be different for the owner, the group, and others.

> Real-world example: A web server user needs access to its own files but shouldn't compromise other users' files on a shared server.

---

## Switching Between Users
- Use the `su` (substitute user) command.

### Requirements:
1. Username to switch to
2. That user's password (unless you're root)

**Example:**
```bash
su -l user2
```
> `-l` starts a shell that mimics logging in directly as that user, including dropping into their home directory.

---

## Common Directories
- `/etc`: System configuration files. Critical root directory.
- `/var`: Variable data like logs and temporary files created by applications.
- `/root`: Home directory for the root (admin) user.
- `/tmp`: Temporary data that doesn't need to persist.

---

✅ *End of Linux Fundamentals Part 2 Notes*

📌 *This room introduced the fundamentals of navigating and interacting with Linux through the terminal. These basics are essential for any cybersecurity or IT professional working in Linux environments.*

