---

## 🕵️‍♂️ Lesson 1: Introduction to Information Gathering (Reconnaissance)

---
###  1. What is Information Gathering?

Information Gathering (also known as **Reconnaissance**) is the process of **collecting data about a target** without actively interacting with or alerting the target system. It is a **passive phase** that lays the foundation for further penetration testing.

---

###  2. Why is it Important?

- It is **one of the most critical phases** in the penetration testing lifecycle.
    
- It helps you understand the **target’s landscape** before launching any technical attacks.
    
- The more accurate your recon is, the more successful and stealthy your attacks will be.
    

---

### 3. When Do You Know You Have Enough Info?

Recon is based on two key **dimensions**:

#### Business Context

- Company assets and services
    
- Publicly available information (e.g., press releases, employee names, job postings)
    
- Competitors and third-party vendors
    
- Business structure (subsidiaries, domains, hosting partners)
    

>  This info helps you **think like an insider** and understand the **“why”** behind the systems.

####  Technical Infrastructure

- IP addresses, subdomains, DNS records
    
- Network ranges and servers
    
- Open ports, services, cloud usage
    
- Public code repositories, forgotten dev environments
    

>  This info builds the **technical attack surface**.

You have enough information **when you can confidently map out the business and technical ecosystem**, identify attack paths, and decide on the next tools or techniques to use.

![[Screenshot 2025-06-07 145206.png|697]]
---

###  4. Pro Tips

-  **Always take notes.** Mind maps, spreadsheets, or note-taking apps like Obsidian can help you track your findings and see connections.
    
-  **Never delete raw data.** Even if something seems unimportant at first, it might become useful later.
    
-  Recon is an **ongoing process** — you may need to go back and dig deeper later in your engagement.
    

---

###  Remember:

- Passive ≠ harmless. Some OSINT techniques can still raise red flags (e.g., excessive DNS lookups).
    
- Information is power — the more you know, the more targeted and efficient your testing can be.
