### 🔎 **3# NMAP - Basic and Stealth Scanning**

---

#### ✅ **Basic Nmap Scan**

- **Command:**
    
    ```bash
    nmap 192.168.1.8
    ```
    
- **Description:**  
    Scans the **1000 most common ports** on the target IP using a **TCP Connect Scan** (default when run without root privileges).
    
- **Note:**  
    TCP Connect scans are **reliable but noisy** — they complete the full TCP handshake and are often logged by firewalls.
    

---

### ⚠️ **Nmap Can Be Intensive**

- Running Nmap on a **Metasploitable** (or any target) can generate **high traffic**.
    
- To **monitor traffic** on the target:
    
    ```bash
    sudo iptables -nvL
    ```
    
    This shows traffic counters for each rule (helps analyze scan load).
    

---

### 🔐 **Restrict Target Machine Traffic (on Metasploitable)**

Use `iptables` to allow only specific IPs to communicate:

```bash
sudo iptables -I INPUT 1 -s 192.168.1.8 -j ACCEPT
sudo iptables -I OUTPUT 1 -d 192.168.1.8 -j ACCEPT
```

[[IPtables]] for more details 😅

---

### 🥷 **Stealth Scan (-sS)**

- **Command:**
    
    ```bash
    sudo nmap 192.168.1.4 -p 25 -sS
    ```
    
- **Wireshark filter:**
    
    ```
    tcp.port == 25 && ip.addr == 192.168.1.4
    ```
    
- **TCP Handshake Seen:**
    
    1. SYN
        
    2. SYN-ACK
        
    3. RST
        
- **Explanation:**  
    Stealth scan sends SYN but does **not complete** the handshake. Faster, and may **bypass firewall logging**.
    

---

### 🔗 **Connect Scan (-sT)**

- **Command:**
    
    ```bash
    nmap 192.168.1.4 -p 25 -sT
    ```
    
- **TCP Flow:**
    
    1. SYN
        
    2. SYN-ACK
        
    3. ACK
        
    4. RST (ends the session)
        
- **Note:**  
    Used when stealth scan isn't possible (e.g., when not running as root). More **detectable**.
    

---

### 🧪 **Firewall Detection Scans**

Used to **detect filtering/firewall presence** rather than open ports:

| Scan Type | Flag  | Notes                                                               |
| --------- | ----- | ------------------------------------------------------------------- |
| ACK Scan  | `-sA` | Checks if ports are filtered (by observing RST or no response)      |
| FIN Scan  | `-sF` | Sends FIN packets — some systems respond differently if no firewall |

---

### 🌐 **UDP Scanning**

- **Slower and less reliable** than TCP scanning.
    
- **Command:**
    
    ```bash
    sudo nmap 192.168.1.4 -sU
    ```
    
- Scan specific UDP port:
    
    ```bash
    sudo nmap 192.168.1.4 -p 137 -sU
    ```
    

#### ⏱️ **UDP Response Interpretations**

| Response                                     | Meaning                                  |
| -------------------------------------------- | ---------------------------------------- |
| **ICMP Port Unreachable**                    | Port is **closed**                       |
| **No Response (retry)**                      | Port is **filtered** (possible firewall) |
| **Service Response (e.g., NetBIOS for 137)** | Port is **open**                         |

#### 🔄 Example Interpretations:

```bash
nmap 192.168.1.4 -p 4444 -sU  → closed (if unreachable)
nmap 192.168.1.4 -p 22 -sU    → closed (if ICMP unreachable)
nmap 192.168.1.4 -p 137 -sU   → open (if it replies with NetBIOS data)
```

---

### 💾 **Save Results**

Because UDP scans are **slow**, you should **save** the output:

```bash
sudo nmap 192.168.1.4 -sU -oN udp_scan_results.txt
```

---

### ✅ Summary of Scan Types:

|Scan Type|Flag|Root Needed?|Detectable?|Notes|
|---|---|---|---|---|
|Connect|-sT|No|Yes|Full TCP handshake|
|Stealth (SYN)|-sS|Yes|No/Low|Incomplete handshake|
|ACK|-sA|Yes|No/Low|Firewall detection|
|FIN|-sF|Yes|No/Low|Evades some stateless FW|
|UDP|-sU|Yes|Yes|Slower, used for UDP services|
