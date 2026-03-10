#kali
## 🧠 **Lesson 1: Linux Basics**

1. **Getting Help:**
    
    - `man ls` – Open the **manual page** for the `ls` command.
        
    - `ls --help` – Display a **quick help message** with usage options.
        
    - `whatis ls` – Show a **one-line summary** of what `ls` does.
        
    - `apropos crack` – Search **manual page descriptions** for the word “crack” (useful when you **forget a command name**).
        
2. **File and Directory Commands:**
    
    - `ls -a` – List **all files**, including hidden ones (`.` and `..`).
        
    - `rm -r dir` – **Recursively delete** a directory and its contents.
        
    - `mkdir dirname` – **Create a new directory** called `dirname`.
        
    - `cp dir1 dir2 -r` – **Copy directories recursively** from `dir1` to `dir2`.
        
3. **IP and Network Information:**
    
    - `ifconfig` – Show **network interface configuration** (older, still used).
        
    - `ip a` – Show **IP addresses** (modern replacement for `ifconfig`).
        
4. **Text Editing and Viewing:**
    
    - `nano file.txt` – Open a file in the **Nano text editor**.
        
    - `cat file.txt` – Display the **contents of the file**.
        
5. **User Management:**
    
    - `sudo adduser` – **Create a new user** with interactive prompts.
        
    - `which adduser` – Find the **path of a command/tool** (only for tools, not regular files).
        
6. **Searching for Files:**
    
    - `locate flag.txt` – Fast search using a **pre-built database** (works for any file).
        
        - ⚠️ Needs updated DB: run `sudo updatedb` to refresh it.
            
    - `find . -name flag.txt` – Powerful command to **search by name, type, permissions, etc.**
        
        - Often used in **post-exploitation** to find sensitive files (e.g. ones owned by root).
            


---

