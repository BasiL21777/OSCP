---

## **Lesson 2: Port Scanning**

---
###  **What Is Port Scanning?**

Port scanning is the process of sending packets to specific ports on a target machine to:

- Discover **open ports**
    
- Identify **running services**
    
- Detect **vulnerabilities or misconfigurations** in these services
    

>  Once open services are identified, attackers can research known **exploits** or perform **manual testing** to check for weaknesses.

---

###  **Why Do Attackers Scan Ports?**

- To fingerprint exposed services (e.g., SSH, HTTP, FTP)
    
- To find **vulnerable versions** of services
    
- To identify misconfigurations (e.g., default credentials, open databases)
    

---

###  **Security Awareness**

If the target admin is **security-aware**, they may use **anti-enumeration techniques**, such as:

- **Changing default ports** (e.g., HTTP from port `80` to `5000`)
    
- **Port knocking**
    
- **Firewalls/IP whitelisting**
    
- **Rate limiting**
    
- **IDS/IPS systems** to detect and block scans
    

>  **Important:** Port scanning **can be noisy** and may trigger security alerts. If you're scanning without permission, it’s considered **illegal and unethical**.

---

###  **TCP vs UDP Scanning**

---

####  **TCP (Transmission Control Protocol)**

- Uses the **3-way handshake**:
    
    1. `SYN` → Client sends request to start connection
        
    2. `SYN/ACK` → Server acknowledges
        
    3. `ACK` → Connection established
        
- **Behavior:**
    
    - If the port is **open** → Target responds with `SYN/ACK`
        
    - If the port is **closed** → Target responds with `RST`
        
- **Fast, reliable, and more common** for scanning.
    

---

####  **UDP (User Datagram Protocol)**

- **Connectionless** protocol — no handshake
    
- Often used for services like DNS, SNMP, and TFTP
    
- **Behavior:**
    
    - If **no response** → The port **may be open or filtered**
        
    - If **ICMP Port Unreachable** is returned → The port is **closed**
        
- **Slower and less reliable** for scanning because:
    
    - No handshake = hard to confirm port status
        
    - Many systems rate-limit or block UDP replies
        
    - Requires longer timeouts to confirm no response ≠ closed
        

>  **GPT Explains Why UDP Scanning Is Slower:**

- Because UDP does **not guarantee delivery or acknowledgment**, scanners must **wait longer** for potential responses or timeouts before determining if the port is open or filtered.
    
- Firewalls may **silently drop** UDP packets, forcing scanners to **wait out the timeout** instead of getting an instant "closed" like with TCP.
    

---

###  **Port Scanning with `nc` (Netcat) and Wireshark**

---

####  **TCP Port Scanning Example**

1. On **target machine (listener)**:
    
    ```bash
    nc -nlvp 1234
    ```
    
2. On **attacker machine (scanner)**:
    
    ```bash
    nc -nvv -w 1 192.168.1.6 1234-1236
    ```
    
    - `-nvv`: verbose
        
    - `-w 1`: 1 second timeout
        
    - Scans TCP ports `1234` to `1236`
        
3. **Monitor with Wireshark**:
    
    - Filter: `tcp.port >= 1234`
        

---

####  **UDP Port Scanning Example**

1. On **target machine (listener)**:
    
    ```bash
    nc -ulvp 1234
    ```
    
2. On **attacker machine (scanner)**:
    
    ```bash
    nc -nvv -u -w 1 -z 192.168.1.6 1234-1236
    ```
    
    - `-u`: use UDP
        
    - `-z`: zero-I/O mode (send packets only)
        
    - `-w 1`: 1 second timeout
        
3. **Monitor with Wireshark**:
    
    - Filter: `udp.port >= 1234`
        

---

###  **Summary**

|Feature|TCP|UDP|
|---|---|---|
|Protocol Type|Connection-oriented (3-way)|Connectionless|
|Speed|Faster|Slower (due to timeouts)|
|Accuracy|High (clear responses)|Lower (uncertain results)|
|Detection|Easier to detect|Harder, but can still be noisy|
|Use Cases|Web, SSH, FTP, etc.|DNS, SNMP, TFTP, etc.|
