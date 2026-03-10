#kali 
Here's your enhanced notes on **File and Command Monitoring**, written in your consistent format and cleaned up for clarity:

---

## File and Command Monitoring**

###  **Log File Monitoring:**

- Some files (like logs) are **dynamically updated** by the system or services.
    
- A good example: Apache access logs
    
    ```bash
    /var/log/apache2/access.log
    ```
    

 **When you:**

- Open browser and type `127.0.0.1` → logs update
    
- Access a path like `127.0.0.1/test` → logs update again
    

###  **Live log tracking with `tail`:**

```bash
tail -f /var/log/apache2/access.log
```

- `-f` → **Follow mode**: keeps watching the file for new lines
    
- Used in **real-time monitoring** of logs
    

---

###  **Command Monitoring with `watch`:**

- `watch` is used to **re-run commands at intervals**
    
- Default interval = **2 seconds**
    

 Example:

```bash
watch free
```

- Displays RAM usage every 2 seconds
    

###  Advanced usage:

```bash
watch -n 0.5 -d free
```

|Option|Meaning|
|---|---|
|`-n`|Set interval in seconds|
|`-d`|Highlight changes in output|

---

###  **Disk Monitoring:**

- `df` → Show disk usage and partitions
    

```bash
df
```

 Monitor it in real-time:

```bash
watch -n 0.5 -d df
```

 While watching `df`, try:

```bash
mv ~/rockyou.txt ~/Desktop
```

- You'll see changes in available disk space.
    
---
[[09 Download Files & Customize Bash Environment|Next]]
