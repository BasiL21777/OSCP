## 🧠 Lesson 5: Domain Background, WHOIS, Netcraft & Reverse IP

---

### 🔍 1. Domain Infrastructure Overview:

Every organization, even small ones, typically has:

|Component|Purpose|
|---|---|
|🌐 **Website**|The public-facing application|
|🖥 **Server**|Hosts website content|
|🔗 **Domain**|Human-readable address (e.g., `grab.com`)|

#### Hosting Models:

- **Cloud Hosting**:
    
    - Providers (AWS, Azure, etc.) assign public IPs.
        
- **On-Premise Hosting**:
    
    - The org contacts their ISP and buys a **static IP**.
        
    - Sets up **DMZ in NAT** to expose the server.
        

#### Domain Registration:

- Handled by registrars like **GoDaddy, Namecheap**.
    
- Domains are mapped to server IPs via **DNS A records**.
    
- Files usually hosted in `/var/www/` on Linux servers.
    

---

### 🧭 2. CIDR and Large Organizations:

- Large enterprises often reserve a **range of IPs (CIDRs)** via ISP.
    
- Example: `193.114.128.0/24` → 256 IPs
    
- These ranges can be linked to an organization’s name and **ASN (Autonomous System Number)**.
    

---

### 🔐 3. WHOIS Lookup:

**Purpose**: Reveal metadata about domain ownership & infrastructure.

|Can Reveal|Examples|
|---|---|
|Registrant Info|Name, Email, Address (if public)|
|Name Servers|DNS providers used|
|IP & Hosting Provider|Where the domain is hosted|

**Command-line Example**:

```bash
whois grab.com
```

🧠 **Note**: If multiple domains are hosted on the same server/IP, an attacker with **RCE on one site** could:

- Escalate privileges
    
- Pivot to other hosted domains (shared environment risk)
    

---

### 🌐 4. Reverse IP Lookup:

**Purpose**: Find other domains hosted on the **same server/IP** (shared hosting risk).

**Tools**:

- Online: `https://viewdns.info/reverseip/`
    
- CLI: `reverseip.py` (custom scripts or APIs)
    

---

## 🔎 Lesson 6: Subdomain Enumeration with Amass, Sublist3r & ASN Mapping

---

### 🏷 1. Domain Typology:

|Type|Example|Description|
|---|---|---|
|**Vertical**|`api.grab.com`, `mail.grab.com`|Subdomains of the same root domain|
|**Horizontal**|`grab.net`, `grab.org`|Different TLDs, often owned by same org|

---

### 🌍 2. ASN & CIDR Concepts:

- **ASN (Autonomous System Number)**:
    
    - Assigned by ISP to uniquely identify an organization’s network on the Internet.
        
    - One ASN may map to multiple **CIDR blocks**.
        

#### 🔧 Useful ASN Tools:

- [BGPView](https://bgp.he.net/dns/grab.com#_ipinfo) → Get ASN and IP info
    
- CLI CIDR fetch:
    

```bash
whois -h whois.radb.net -- '-i origin AS16509' | grep "route" > grab-CIDRs.txt
```

---

### 🛠 3. Amass (Advanced Subdomain Enumeration Tool)

**Intel Gathering Examples**:

```bash
amass intel -org grab.com            # Get info about org
amass intel -asn 16509               # Discover domains tied to ASN
amass intel -cidr 3.0.0.0/15         # List domains within IP block
amass intel -whois -d grab.com       # Domains registered by same owner
```

---

### 🌐 4. Subdomain Enumeration:

|Mode|Description|
|---|---|
|**Passive**|Uses OSINT, cached sources (faster, but may include dead domains)|
|**Active**|Sends DNS queries (slower, but real-time data)|

```bash
amass enum -passive -d grab.com
amass enum -active -d grab.com
```

🧪 Use both methods and compare results for accuracy.

---

### 🔎 5. Sublist3r:

Simple Python-based tool for subdomain enumeration.

```bash
sublister -d grab.com -o grab.txt
```

---

### 📌 Summary Table:

|Tool|Purpose|
|---|---|
|`whois`|Domain registration and owner info|
|`reverse IP`|Other domains on same IP|
|`Amass intel`|Enumerate domains via org, CIDR, ASN|
|`Amass enum`|Subdomain discovery (active/passive)|
|`Sublist3r`|Lightweight subdomain scanner|
|`bgp.he.net`|IP ownership, ASN lookup|
