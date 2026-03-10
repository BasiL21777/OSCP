## 🌐 Lesson 2: Website Recon (Passive Recon on Web Targets)

---

### 🔍 1. What Is Website Recon?

Website Recon is the process of **gathering information from a target's official website and related online presence**. It is a goldmine for both **business** and **technical intelligence**, and usually the **first step in real-world recon**.

---

### 🎯 2. Why Focus on the Website?

- It’s **public-facing** and often contains **a lot of unintentional disclosures**.
    
- It helps you understand the **structure**, **users**, and **technologies** behind the target.
    
- Even if the website itself isn't vulnerable, it can **lead to other potential attack surfaces** (e.g., third-party vendors, login portals, infrastructure insights).
    
---
### 🧠 3. What to Look For?

#### 🧾 Pages to Explore:

- `/about-us`, `/contact`, `/support`, `/careers`, `/press`, `/partners`, `/login`
    
- These can reveal:
    
    - Internal roles and names
        
    - Email formats (e.g., `john.doe@company.com`)
        
    - Third-party tools
        
    - Login panels
        
    - Internal naming conventions
        
    - Organizational structure
        

#### 🧑‍💼 Multiple User Privilege Types:

- Test with different roles in mind:
    
    - Admin panels
        
    - Client portals
        
    - Partner logins
        
    - Beta or dev environments
        
- Example: Check if `admin.company.com` exists if `login.company.com` does.
    

#### 🤝 Third Parties & Partnerships:

- Look for:
    
    - Technology stack mentions (e.g., AWS, Atlassian, Salesforce)
        
    - Merger/acquisition info (e.g., Facebook acquiring Instagram)
        
    - Vendors mentioned in footers or job postings
        
    - Certifications, compliance vendors, or SSO providers
        
- 📍 Use tools like [Crunchbase](https://www.crunchbase.com/) or [Agiliance](https://www.agiliance.com/) to check M&A data.
    

> 💡 If the target uses a **trusted third-party**, attacking that vendor might be an alternative path (e.g., supply chain attacks, trust exploitation).


---

### 💼 4. Use Job Listings (Especially LinkedIn)

Job postings can reveal:

- Internal systems and stacks (e.g., “Must know Kubernetes, Django, Azure”)
    
- Open positions (e.g., multiple security job listings could mean **security is a concern** or they’ve been recently breached)
    
- Project stages (e.g., “Help us migrate to microservices” gives tech direction)
    

Tools:

- LinkedIn (company page → jobs)
    
- Indeed, Glassdoor, Careers page
    

---

### ⚠️ 5. Why Does This Matter?

- You may **not find vulnerabilities** in the primary target...
    
- But if that target **trusts** another service or vendor, **attacking the trusted source** (e.g., through phishing, weak APIs, or social engineering) may lead back to the main target.
    
- This is known as **“pivoting”** — from partner to target.
    

---

### 🛠 Tools & Techniques

- `whatweb` / `wappalyzer` — for tech stack detection
    
- `waybackurls`, `gau`, `urlscan.io` — for historical URLs
    
- `theHarvester` — for emails/domains/subdomains
    
- `crt.sh`, `censys.io`, `shodan.io` — for certificates, IPs, infrastructure
    
