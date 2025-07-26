
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

