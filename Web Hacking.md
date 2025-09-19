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
```
