# 🧑‍🍳 CyberChef: The Basics

CyberChef is a simple, intuitive web-based application designed to help with various “cyber” operation tasks within your web browser. Think of it as a **Swiss Army knife for data** — a toolbox of different tools designed to do specific tasks. These tasks range from simple encodings like XOR or Base64 to complex operations like AES encryption or RSA decryption. CyberChef operates on **recipes**, a series of operations executed in order.

---

## 🧩 The Four Main Areas of CyberChef

CyberChef consists of four areas, each with distinct components and features:

1. **Operations**
2. **Recipe**
3. **Input**
4. **Output**

---

## ⚙️ Operations Area

This area is a repository of all operations that CyberChef can perform, organized into categories for easy access. You can search for operations to quickly find what you need.

### Common Operations

| Operation | Description | Example |
|------------|--------------|----------|
| From Morse Code | Translates Morse Code into (upper case) alphanumeric characters. | `- .... .-. . .- - ...` → `THREATS` |
| URL Encode | Encodes problematic characters into percent-encoding format. | `https://tryhackme.com/r/room/cyberchefbasics` → `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics` |
| To Base64 | Encodes raw data into an ASCII Base64 string. | `This is fun!` → `VGhpcyBpcyBmdW4h` |
| To Hex | Converts text to hexadecimal bytes separated by a delimiter. | `This Hex conversion is awesome!` → `54 68 69 73 20 48 ...` |
| To Decimal | Converts text to its ordinal integer array. | `This Decimal conversion is awesome!` → `84 104 105 115 ...` |
| ROT13 | Simple Caesar cipher rotating characters by 13. | `Digital Forensics` → `Qvtvgny Sberafvpf` |

Hovering over an operation provides a sample, description, or link to Wikipedia for context.

---

## 🧪 Recipe Area

The **Recipe Area** is the heart of CyberChef. Here you can select, arrange, and customize operations to suit your task.

### Features

- **Save Recipe:** Save selected operations.  
- **Load Recipe:** Load previously saved recipes.  
- **Clear Recipe:** Clear the current recipe.  
- **BAKE! Button:** Executes the operations on the input.  
- **Auto Bake:** Automatically runs the recipe when changes occur.

---

## ✍️ Input Area

The input area allows you to paste, type, or drag text/files for processing.

### Features

- **Add new input tab**
- **Open folder as input**
- **Open file as input**
- **Clear input/output**
- **Reset pane layout**

---

## 💡 Output Area

Displays the processed results after the recipe runs.

### Features

- **Save output to file (.dat)**  
- **Copy raw output**  
- **Replace input with output**  
- **Maximize output pane**

---

## 🧠 CyberChef Thought Process

Before you start, use this 4-step workflow:

1. **Set a clear objective** — What do you want to achieve?  
   Example: “I found a gibberish string; I want to know what it contains.”  
2. **Input your data** — Paste or upload your data.  
3. **Select operations** — Choose operations (e.g., Base64, ROT13, URL Decode).  
4. **Check the output** — If the result isn’t right, adjust and repeat.

---

## 🧰 Common Operation Categories

### 🧭 Extractors

| Operation | Description |
|------------|--------------|
| Extract IP addresses | Extracts all IPv4 and IPv6 addresses. |
| Extract URLs | Extracts URLs (requires protocol for accuracy). |
| Extract email addresses | Extracts all email addresses in the form `name@domain.com`. |

---

### ⏰ Date and Time

| Operation | Description |
|------------|--------------|
| From UNIX Timestamp | Converts UNIX timestamp → readable datetime. |
| To UNIX Timestamp | Converts datetime → UNIX timestamp. |

Example:  
`Fri Sep 6 20:30:22 +04 2024` → `1725654622`

---

### 💾 Data Format

| Operation | Description | Example |
|------------|--------------|----------|
| From Base64 | Decodes Base64 to raw data. | `V2VsY29tZSB0byB0cnloYWNrbWUh` → `Welcome to tryhackme!` |
| URL Decode | Converts percent-encoded characters. | `%3A` → `:` |
| From Base85 | Decodes ASCII Base85 string. | `BOu!rD]j7BEbo7` → `hello world` |
| From Base58 | Decodes Base58 string (no l, I, 0, O). | `AXLU7qR` → `Thm58` |
| To Base62 | Encodes binary → Base62 ASCII. | `Thm62` → `6NiRkOY` |

---

## 🔢 Base64 Encoding (Manual Walkthrough)

Example: Encoding “THM”.

1. **Convert to Binary**  
   - T = `01010100`, H = `01001000`, M = `01001101`  
   → Combined: `010101000100100001001101`

2. **Split into 6-bit groups → Convert to Decimal**  
   `010101 000100 100001 001101` → 21, 4, 33, 13

3. **Map Decimal to Base64 Table**  
   | Decimal | Character |
   |----------|------------|
   | 21 | V |
   | 4 | E |
   | 33 | h |
   | 13 | N |

   ✅ Final Base64 = `VEhN`

---

### 🌐 URL Decode Quick Reference

| Character | UTF-8 Code |
|------------|-------------|
| : | %3A |
| / | %2F |
| . | %2E |
| = | %3D |
| # | %23 |

---

## 🏁 Summary

CyberChef is a **powerful all-in-one data transformation and analysis tool**. Whether you’re decoding Base64, analyzing URLs, or extracting data, its visual interface simplifies complex processes. While CyberChef excels at manual and small-scale processing, for large-scale automation, consider pairing it with dedicated tools or scripts.
