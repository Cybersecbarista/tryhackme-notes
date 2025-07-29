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

📌 *This room introduced the fundamentals of navigating and interacting with Linux through the terminal. These basics are essential for any cybersecurity or IT professional working in Linux environments.*

