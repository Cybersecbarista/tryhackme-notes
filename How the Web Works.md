
# DNS in Detail

The **Domain Name System (DNS)** provides a simple way to communicate with devices on the internet without needing to remember complex IP addresses. Instead of using a number, DNS allows us to use human-readable domain names.

---

## 🧭 Domain Hierarchy

### 🔹 Top-Level Domain (TLD)
- The **TLD** is the rightmost part of the domain name, such as:
  - `.com`, `.gov`, `.edu`, `.mil`, `.org`
- There are two types of TLDs:
  - **gTLD** (Generic Top-Level Domain) — Indicates the purpose of the domain  
    - Example: `.com` (commercial), `.edu` (education)
  - **ccTLD** (Country Code Top-Level Domain) — Indicates geographical region  
    - Example: `.ca` (Canada), `.co.uk` (United Kingdom)

---

### 🔹 Second-Level Domain
- This is the name of the website, such as `tryhackme` or `google`
- Limited to **633 characters**
- Can include:
  - Lowercase letters `a–z`
  - Numbers `0–9`
  - Hyphens `-`

---

### 🔹 Subdomain
- Appears to the **left** of the second-level domain, separated by a dot
- Example: `admin.tryhackme.com` → `admin` is the subdomain
- Can use multiple subdomains like:  
  `jupiter.servers.tryhackme.com`
- Character limit: **2533 characters total**
- No limit to the number of subdomains

---

## 📄 DNS Record Types

DNS isn't just for websites — it supports multiple record types used for different services and purposes.

| Record Type | Description |
|-------------|-------------|
| `A`         | Resolves a domain to an **IPv4 address** (e.g., `104.26.10.229`) |
| `AAAA`      | Resolves a domain to an **IPv6 address** (e.g., `2606:4700:20::681a:be5`) |
| `CNAME`     | Maps one domain to **another domain name** (e.g., `store.tryhackme.com` → `shops.shopify.com`) |
| `MX`        | Specifies **mail servers** for email delivery (e.g., `alt1.aspmx.l.google.com`) — includes a **priority flag** for failover |
| `TXT`       | Contains **text-based data**, often used for:
  - Domain ownership verification
  - SPF/DKIM (email validation)
  - General metadata

---

## 🌐 What Happens When You Make a DNS Request

1. **Local Cache Check**  
   Your computer first checks its **local DNS cache** to see if it already knows the address.

2. **Recursive DNS Server**  
   If not found locally, it asks the **recursive DNS server** (usually provided by your ISP, or custom like Google DNS `8.8.8.8`).

3. **Root DNS Servers**  
   If the recursive server doesn’t know, it contacts the **root DNS servers** which direct it to the correct **Top-Level Domain (TLD) server** (e.g., `.com`).

4. **TLD Server → Authoritative Nameserver**  
   The **TLD server** returns the location of the **authoritative nameserver** for that domain (e.g., `kip.ns.cloudflare.com` for `tryhackme.com`).

5. **Authoritative DNS Server → DNS Record**  
   This server contains the actual DNS records. The recursive server retrieves the record and caches it based on the **TTL** (Time To Live) value, then returns the result to your device.

---

## 🔁 Caching and TTL

- All DNS records come with a **TTL (Time To Live)** value.
- TTL determines how long the record is **cached** locally or by recursive DNS servers.
- Caching speeds up requests by avoiding repeated full lookups for frequently visited sites.

---

## ✅ Summary

DNS is a core internet protocol that maps human-readable names to machine-usable IP addresses. Understanding how it works — from domain structure to record types and DNS resolution — is essential for networking and cybersecurity.

# HTTP in Detail

## What is HTTP? (HyperText Transfer Protocol)

HTTP is the protocol used whenever you view a website. It was developed by Tim Berners-Lee and his team between 1989–1991. HTTP defines the rules for communicating with web servers to transmit webpage data such as HTML, images, and videos.

---

## What is HTTPS? (HyperText Transfer Protocol Secure)

HTTPS is the secure version of HTTP. It:
- Encrypts data in transit
- Prevents data from being intercepted
- Verifies that the server is legitimate (not an impersonator)

---

## Requests and Responses

When we access a website, the browser makes **HTTP requests** to the web server for content like HTML, images, videos, etc. The server then returns **HTTP responses**.

---

## What is a URL? (Uniform Resource Locator)

A URL is an instruction for accessing a resource on the internet.

### URL Components:
- **Scheme**: Protocol to use (e.g. `http`, `https`, `ftp`)
- **User**: Optional credentials (username/password)
- **Host**: Domain name or IP address of the server
- **Port**: Port number (default is 80 for HTTP, 443 for HTTPS)
- **Path**: File or directory to access
- **Query String**: Additional data (`?id=1`)
- **Fragment**: In-page reference (`#section1`)

---

## Making a Request

Basic HTTP request example:


- Line 1: GET method, root path `/`, HTTP version
- Line 2: Target host
- Line 3: Browser details
- Line 4: Referrer page
- Line 5 (not shown): Blank line to mark end of request

---

## HTTP Methods

HTTP methods indicate the action the client wants to perform.

| Method | Description |
|--------|-------------|
| `GET` | Retrieve data from a server |
| `POST` | Send data to create a new record |
| `PUT` | Send data to update an existing record |
| `DELETE` | Remove a record or resource |

---

## HTTP Status Codes

Status codes inform the client of the result of the request.

### Status Code Categories:
- **100–199**: Informational (rarely used)
- **200–299**: Success
- **300–399**: Redirection
- **400–499**: Client error
- **500–599**: Server error

### Common Status Codes:
| Code | Meaning |
|------|---------|
| `200 OK` | Request successful |
| `201 Created` | New resource created |
| `301 Moved Permanently` | Resource has moved permanently |
| `302 Found` | Resource temporarily at a different location |
| `400 Bad Request` | Malformed request |
| `401 Unauthorized` | Login required |
| `403 Forbidden` | Access denied |
| `404 Not Found` | Resource not found |
| `405 Method Not Allowed` | Invalid HTTP method used |
| `500 Internal Server Error` | General server failure |
| `503 Service Unavailable` | Server overloaded or under maintenance |

---

## HTTP Headers

Headers provide additional information in requests and responses.

### 🔹 Common Request Headers
| Header | Description |
|--------|-------------|
| `Host` | Specifies target domain |
| `User-Agent` | Identifies browser and version |
| `Content-Length` | Size of data being sent (e.g., form submissions) |
| `Accept-Encoding` | Supported compression types (e.g., gzip) |
| `Cookie` | Sends stored cookies to the server |

---

### 🔸 Common Response Headers
| Header | Description |
|--------|-------------|
| `Set-Cookie` | Sends cookies to be stored by the client |
| `Cache-Control` | Caching instructions |
| `Content-Type` | Type of data returned (HTML, CSS, JSON, etc.) |
| `Content-Encoding` | Compression method used on response data |

---

## Cookies

Cookies are small pieces of data stored by the browser.

- Sent by the server using the `Set-Cookie` header
- Returned by the client in future requests via the `Cookie` header
- Used to maintain **session state**, remember preferences, or track behavior

### Key Points:
- HTTP is stateless; cookies help track sessions
- Cookies often store **tokens** (not plaintext passwords)
- Used heavily for authentication and personalization

---
# 🌐 How the Web Works

When you visit a website, your browser (like Safari or Google Chrome) makes a request to a web server asking for information about the page you're visiting. The server responds with data that your browser uses to display the page. A web server is simply a dedicated computer located elsewhere in the world that handles these requests.

There are two major components that make up a website:

- **Front End (Client-Side):** The way your browser renders a website.
- **Back End (Server-Side):** A server that processes your request and returns a response.

There are many processes involved in how your browser makes a request to a web server, but the core concept is: the browser makes a request, and the server responds with data your browser uses to render content.

---

## 🧱 HTML

Websites are primarily created using the following core technologies:

- **HTML** – Builds and defines the structure of a website.
- **CSS** – Styles the website to make it visually appealing.
- **JavaScript** – Adds interactivity and dynamic features.

HTML (HyperText Markup Language) is the standard language for creating web pages. HTML is composed of elements, also called tags, which define the content and structure. Tags can contain attributes that provide additional context or control appearance/behavior.

Some common attributes include `class`, used to apply CSS styles; `src`, used to define the source for media like images or scripts; and `id`, a unique identifier for a given element.

An element can have multiple attributes, and while classes can be shared across elements, each `id` must be unique within a page. IDs are often used for JavaScript interaction and specific styling.

You can inspect or view the HTML of any website by right-clicking the page and selecting “View Page Source” in Chrome or “Show Page Source” in Safari.

---

## ⚙️ JavaScript

JavaScript (JS) is one of the most widely used programming languages in web development. It enables interactivity and dynamic content on otherwise static HTML pages.

HTML defines the structure of a page, while JavaScript controls functionality. Without JavaScript, a web page is static and unresponsive to user input. With JavaScript, developers can dynamically update content, change styles in real-time, handle events like clicks or mouse movements, create animations, and perform client-side validation.

JavaScript can be embedded directly in a web page using script tags or linked externally using a `src` attribute. HTML elements can also include event listeners like `onclick` or `onhover`, which trigger JavaScript actions when events occur.

---

## 🔐 Sensitive Data Exposure

Sensitive Data Exposure happens when a website fails to protect or remove sensitive information, and that data becomes visible in the frontend source code. Since much of a website’s content is rendered on the client side using HTML, careless developers may accidentally leave behind sensitive data such as login credentials, hidden admin or debug links, API keys, or tokens.

This information can be viewed by anyone using “View Page Source” or browser developer tools. Attackers can potentially leverage exposed data to escalate privileges or access protected areas of the application.

As part of any web security assessment, it’s important to review source code for exposed secrets, hidden paths, or misconfigurations.

---

## 💉 HTML Injection

HTML Injection is a client-side vulnerability that occurs when unsanitized user input is rendered directly into a web page’s HTML. This can allow an attacker to inject malicious HTML or JavaScript, which may alter the appearance or behavior of a page.

If a web application takes user input and reflects it without proper filtering, attackers can modify what the page displays and potentially even execute scripts if JavaScript is allowed.

User input is often reused in frontend and backend functions. If that input is inserted into the page without proper validation or escaping, HTML injection occurs.

To prevent this vulnerability, developers should never trust user input. It must be sanitized and validated on both frontend and backend before being used. Dangerous characters or tags should be stripped, encoded, or filtered out, and proper input handling should be enforced across all components.

---

## ✅ Summary

- Websites operate on a request-response model between the browser and web server.
- HTML builds the structure, CSS styles it, and JavaScript makes it interactive.
- JavaScript can update content, react to events, and dynamically control page behavior.
- Sensitive Data Exposure occurs when private data is visible in public frontend code.
- HTML Injection exploits unsanitized input to alter page content or behavior.
- Input should always be treated as untrusted and must be sanitized and validated properly.

---
# 🌐 Putting It All Together & How the Web Works

## 🧠 Summary of the Web Workflow

When you request a webpage in your browser:

1. Your computer needs the **IP address** of the server → uses **DNS**.
2. It communicates using **HTTP** or **HTTPS** protocols.
3. The server responds with:
   - HTML
   - CSS
   - JavaScript
   - Images, etc.
4. Your **browser renders** the data to display the website.

---

## ⚖️ Load Balancers

Used when:
- Websites have **high traffic**.
- Applications require **high availability**.

### Key Functions:
- Distributes traffic across **multiple servers**.
- Provides **failover** if one server becomes unresponsive.

### Algorithms:
- **Round-Robin**: Rotates through servers.
- **Weighted**: Sends traffic to the least busy server.

### Health Checks:
- Regularly checks if servers are healthy.
- Stops sending traffic to a server that fails health checks.

---

## 🌍 CDN (Content Delivery Network)

- Hosts **static files** (JavaScript, CSS, images, videos) on globally distributed servers.
- Sends user requests to the **closest geographical server**.
- Reduces **latency**, **server load**, and increases **site speed**.

---

## 🗃️ Databases

Websites use databases to **store and retrieve** user and app data.

### Common Types:
- **MySQL**
- **MSSQL**
- **MongoDB**
- **PostgreSQL**

Databases can range from:
- Simple plain text files
- To complex, multi-server clusters

---

## 🔥 WAF (Web Application Firewall)

A **WAF** sits between the client and the server.

### Main Functions:
- Protects against **hacking attempts**, **DoS attacks**, and **malicious bots**.
- Filters incoming traffic using:
  - **Pattern matching**
  - **Browser verification**
  - **Rate limiting** (blocks excessive requests per IP)

If a request is deemed dangerous, it's dropped before it reaches the server.

---

## 🖥️ What Is a Web Server?

A **web server** is software that:
- Listens for incoming HTTP(S) connections
- Delivers requested content (HTML, files, images) to users

### Common Web Server Software:
- **Apache**
- **Nginx**
- **IIS** (Windows)
- **NodeJS**

### Default Root Directories:
- **Linux (Apache/Nginx):** `/var/www/html`
- **Windows (IIS):** `C:\inetpub\wwwroot`


---

## 🌐 Virtual Hosts

A single web server can **host multiple websites** using different domain names.

### How It Works:
- The server inspects the **hostname** in the HTTP headers.
- Matches it to a **virtual host config**.
- Serves the corresponding site.

### Example Configs:
- `one.com` → `/var/www/website_one`
- `two.com` → `/var/www/website_two`

If no match is found → the **default site** is served.

> ✅ There's no limit to how many virtual hosts you can configure.

---

## 🧱 Static vs Dynamic Content

### 🔒 Static Content
- **Unchanging** content directly served from the server.
- Examples:
  - Images
  - CSS
  - JavaScript
  - HTML files that don’t change

Served **as-is** without any processing.

---

### 🔄 Dynamic Content
- Changes based on:
  - **User input**
  - **Database entries**
  - **App logic**

#### Examples:
- Blog showing latest posts
- Search results
- User dashboards

Content is generated in the **backend**, then rendered and delivered to the **frontend** (the user’s browser).

---

## 🧠 Backend & Scripting Languages

Backend languages **power the server-side logic** that handles requests, processes data, and builds custom responses.

### Common Backend Languages:
- **PHP**
- **Python**
- **Ruby**
- **NodeJS**
- **Perl**

### What Backend Code Can Do:
- Connect to and query **databases**
- Handle **user input**
- Call **external APIs**
- Generate **dynamic HTML**
- Validate data and enforce business rules

> ⚙️ While the backend logic is hidden, the result is visible in the form of structured, dynamic content shown on the **frontend**.

---






