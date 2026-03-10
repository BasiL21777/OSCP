#kali 
Perfect! Here's your **#7 Download Files** and **#8 Customize Bash Environment** sections, cleaned up and enhanced in your existing note-taking format:

---

##  **Download Files**

###  **wget – Download from URL**

```bash
wget <file_url>
wget <file_url> -O <new_name>
```

- Downloads the file with the same name (unless renamed with `-O`)
    
-  **Timestamp stays as the server's upload time**
    

 _Why this matters:_  
If you download a backup and find credentials, knowing **when it was uploaded** (not when you downloaded it) is critical — use `wget` for accuracy.

---

### **curl – Command-line Browser**

```bash
curl "<url>" -o <file_name>
```

- Works like a browser without GUI
    
- Can send **GET, POST, etc.**
    
-  Timestamp is the **download time on your machine**
    

---

###  **axel – Fast Downloader**

```bash
axel "<URL>" -n 20 -a -o pala.png
```

| Option | Meaning                        |
| ------ | ------------------------------ |
| `-n`   | Number of connections (faster) |
| `-a`   | Show progress bar              |
| `-o`   | Output file name               |

-  Timestamp = your local time
    
- Great for **large files** or slow servers
    

---

###  **git clone – Download from GitHub**

```bash
git clone <repo_url>
```

- Clones a full GitHub repo locally (including history)
    

---

 **Quick Recap: Timestamp Importance**

- Browser / curl / axel = time reflects **when you downloaded**
    
- wget = keeps **server upload time**
    
- Crucial for forensic or backup investigations
    

---

##  **Customize Bash Environment**

###  **Clean up your command history**

```bash
export HISTIGNORE="&:ls:cd:cd ..:clear:cls:history:exit"
```

- Prevents certain commands from being saved in `~/.bash_history`
    
- `&` → ignore repeated last command
    
- This helps **focus only on important or unique commands**
    
