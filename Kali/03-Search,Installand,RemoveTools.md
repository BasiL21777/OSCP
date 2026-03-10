#kali
## **Lesson 3: Search, Install, and Remove Tools**

1. **APT (Advanced Package Tool)** – Main package manager in Debian-based systems like Kali.
    
2. **Update and Upgrade:**
    
    - `sudo apt update` – **Refresh package list** and available updates.
        
    - `sudo apt upgrade` – **Install updates** for all installed packages (takes time).
        
3. **Install, Show, and Search Packages:**
    
    - `sudo apt show apache2` – Show detailed **info about a package**.
        
    - `sudo apt search apache2` – **Search for packages** with "apache2" in the name.
        
    - `sudo apt install apache2` – **Install** Apache2 (or upgrade if already installed).
        
4. **Remove Packages:**
    
    - `sudo apt remove apache2` – Remove Apache2.
        
    - `sudo apt remove --purge apache2` – Remove **including config files**.
        
5. **Installing with `dpkg`:**
    
    - Some tools aren't available via APT.
        
    - Use: `sudo dpkg -i tool.deb` – Install a `.deb` package **manually**.
        
        - You need to **download the package first**.
            

---
[[04 Bash Environment|Next]]
