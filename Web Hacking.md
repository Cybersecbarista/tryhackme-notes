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
