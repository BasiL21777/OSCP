---

## **Lesson 1: DNS Enumeration**

---
### 🔹 **1. Basics of DNS**

---

#### ✅ **What is DNS?**

- DNS (Domain Name System) is like a **phonebook for the internet**. It translates domain names (like `google.com`) into IP addresses.
    
- DNS records are stored like entries in a database.
    
- If an attacker **modifies DNS records**, they can redirect users to **malicious websites** — a major security risk.
    

#### ✅ **How DNS Works**

1. **Browser checks cache** for recent domain-IP mappings.
    
2. If not found, it checks the **`/etc/hosts`** file (on Linux).
    
3. If still not found, it queries the **configured DNS server**.
    

> ⚠️ **DNS can be attacked**, and misconfigurations can expose valuable information.

---

#### ✅ **Common DNS Record Types**

|Type|Description|Example|
|---|---|---|
|`A`|Maps hostname to IP (forward lookup)|`host -t a google.com`|
|`PTR`|Maps IP to hostname (reverse lookup)|`host -t ptr 8.8.8.8`|
|`CNAME`|Maps alias to hostname|(e.g., www → main.example.com)|
|`MX`|Mail exchange servers|`host -t mx google.com`|

> ℹ️ Use `host` for simple queries. `dig` provides more advanced options.

---

### 🔹 **2. Brute Force DNS Lookups**

---

#### 🔸 **Forward Brute Force Lookup**

Try to find subdomains using a wordlist:

```bash
for sub in $(cat /usr/share/wordlists/seclists/Discovery/DNS/fierce-hostlist.txt); do
  host -t a $sub.megacorpone.com | grep -v "not found"
done
```

#### 🔸 **Reverse Brute Force Lookup**

Check a subnet for hostnames:

```bash
for n in {1..255}; do
  host -t ptr 167.114.21.$n | grep -v "not found" | grep "megacorpone"
done
```

> ⚠️ Not all IPs return valid hostnames. Some may belong to unrelated services (e.g., CloudFront).

**Example:**

```bash
host -t a grab.com         # → 108.159.102.34
host -t ptr 108.159.102.34 # → cloudfront.net (not related to grab.com)
```

---

### 🔹 **3. DNS Zone Transfer (AXFR)**

#### ✅ **What Is It?**

- Zone Transfer dumps the full DNS database (zone file) of a domain.
    
- Normally **restricted**, but **misconfigured servers** may allow it.
    
- Can reveal:
    
    - Internal hosts
        
    - IP addresses
        
    - Services and infrastructure
        

---

#### ✅ **Steps to Perform Zone Transfer**

1. **Find name servers (NS):**
    

```bash
host -t ns megacorpone.com
```

2. **Attempt zone transfer from each NS:**
    

```bash
host -l megacorpone.com ns3.megacorpone.com
```

> ❗ Try other NS entries (`ns1`, `ns2`, etc.) if one fails.

---

#### ✅ **Automated Bash Script**

```bash
#!/bin/bash
if [ -z "$1" ]; then
  echo "[*] Usage: $0 domain.com"
  exit 0
fi

for ns in $(host -t ns $1 | cut -d " " -f 4); do
  host -l $1 $ns | grep "has address"
done
```

---

#### ✅ **Zone Transfer Tools**

|Tool|Usage|
|---|---|
|`dnsrecon`|`dnsrecon -d megacorpone.com -t axfr`|
|`dnsenum`|`dnsenum -d megacorpone.com -D dns_wordlist.txt`|

> `-D` flag in `dnsenum` specifies a subdomain brute-force wordlist.

---

### ✅ **Summary**

DNS enumeration is a powerful technique used during **active reconnaissance** to map domain names, discover subdomains, reveal misconfigurations, and even retrieve internal infrastructure through zone transfers.

---

Would you like me to turn this into a PDF or add diagrams/visual flow for DNS resolution and zone transfer?