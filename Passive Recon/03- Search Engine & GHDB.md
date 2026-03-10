---

## 🌐 Lesson 4: Search Engines & GHDB (Google Hacking Database)

---
### 🎯 1. Purpose:

Use **Google Dorks** to extract hidden, sensitive, or indexed information from search engines about your target without direct interaction. It's a **passive reconnaissance technique**.

---

### 🔍 2. Useful Google Dork Operators:

| Dork        | Description                                                    | Example                         |
| ----------- | -------------------------------------------------------------- | ------------------------------- |
| `site:`     | Search within a specific domain and subdomains                 | `site:example.com`              |
| `link:`     | Find pages linking **to** the target domain                    | `link:example.com`              |
| `intext:`   | Search pages that contain specific **text**                    | `intext:example.com`            |
| `intitle:`  | Search for pages with specific **titles**                      | `intitle:"Login Page"`          |
| `filetype:` | Search for specific file types (PDF, DB, XLS, etc.)            | `filetype:pdf site:example.com` |
| `cache:`    | View the **cached version** of a site (useful for old content) | `cache:example.com`             |
| `inurl:`    | Search for keywords in URLs                                    | `inurl:admin site:example.com`  |

---

### 🧩 3. Logical Operators:

| Operator     | Description                          | Example                             |
| ------------ | ------------------------------------ | ----------------------------------- |
| `AND` / `OR` | Combine search terms                 | `intext:admin AND site:example.com` |
| `-`          | Exclude specific terms or subdomains | `site:example.com -www`             |
| `+`          | Force inclusion (rarely used now)    | `+login`                            |
| `""`         | Exact match for phrases              | `"admin login"`                     |

---

### 🛠 4. Practical Examples:

- `site:example.com filetype:sql` → Find exposed database dumps
    
- `intext:"© Grab 2025"` → Search for a **unique site signature**
    
- `intitle:"index of" "parent directory"` → Find **directory listings** (often include backups, config files, etc.)
    
- `filetype:xls OR filetype:csv inurl:admin` → Find sensitive spreadsheets with possible credentials
    

---

### 💀 5. “Evil” Dorks (Be Responsible ⚠️):

These dorks may uncover **misconfigured or exposed** data:

- `intitle:"index of" "parent directory"` → Open directory listings
    
- `filetype:env OR filetype:bak site:example.com` → Exposed backups
    
- `inurl:admin login` → Admin login panels
    
- `filetype:log site:example.com` → Server logs
    

---

### 📚 6. GHDB (Google Hacking Database):

- A large collection of curated Google Dorks
    
- Maintained by **Exploit-DB**
    
- Search for:
    
    - Exposed credentials
        
    - Misconfigured admin panels
        
    - Sensitive files
        
- URL: [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)
    

---

### 🧰 7. Additional Tools:

#### 🔎 FOCA (Windows):

- Scans a domain for publicly exposed documents (PDF, DOCX, XLS, etc.)
    
- Extracts **metadata** like usernames, emails, paths
    
- Useful in footprinting phase
    

#### ⏳ Wayback Machine (Archive.org):

- View archived versions of websites
    
- Identify **removed directories, endpoints, old tech stacks**
    
- URL: [https://archive.org/web](https://archive.org/web)
    

#### 🛠 Wayback CLI Tool:

- Written in Go
    
- Fast enumeration of historical URLs for a domain
    
- GitHub Repo: `https://github.com/tomnomnom/waybackurls`
    

```bash
echo "example.com" | waybackurls > urls.txt
```

---

### ✅ Summary:

| Tool / Dork          | Purpose                         |
| -------------------- | ------------------------------- |
| `site:`, `filetype:` | Identify exposed documents      |
| `intitle:`, `inurl:` | Discover admin panels, backups  |
| GHDB                 | Ready-made dork repository      |
| FOCA                 | Metadata extraction from files  |
| Wayback Machine      | Discover old or deleted content |

