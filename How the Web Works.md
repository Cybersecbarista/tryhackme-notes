
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

