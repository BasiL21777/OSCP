#kali
##  **Lesson 2: Managing Kali Services**

1. Kali comes with various services like **SSH**, **HTTP**, etc.
    
2. By default, most are **disabled**.
    
3. **Always change default passwords** for security:
    
    - `passwd` – Change your current user's password.
        
4. **Using `systemctl`:**
    
    - `sudo systemctl enable ssh` – Enable SSH to **start on boot**.
        
    - `sudo systemctl start ssh` – **Start SSH service immediately**.
        
    - `sudo systemctl status ssh` – Check if SSH is running.
        
    - `sudo systemctl stop ssh` – Stop the SSH service.
        
5. **Alternative: Using `service` command:**
    
    - `sudo service ssh start` – Start the SSH service.
        
    - `sudo service ssh status` – Check status.
        
    - `sudo service ssh stop` – Stop it.
        
6. **List all services:**
    
    - `service --status-all` – List **all service statuses**.
        
        - Use `| grep +` to filter and show only active ones.
            
7. **SSH into a machine:**
    
    - `ssh username@ip_address` – Connect to a remote system via SSH.

    - [[SSH]] : for more info
        

---
### **[[03-Search,Installand,RemoveTools|Next]]**
