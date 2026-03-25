## **What is `ffuf`?**

`ffuf` (Fuzz Faster U Fool) is a **fast, flexible, and powerful fuzzing tool** used for discovering hidden files, directories, subdomains, parameters, and other attack vectors on a web server. It is widely used in **penetration testing** and **bug bounty hunting** to automate brute-force attacks.

It is known for:

- **Speed**: Uses multi-threading for rapid fuzzing.
    
- **Customization**: Allows custom wordlists, filtering, and recursion.
    
- **Support for multiple protocols**: Works with **HTTP, HTTPS, and raw data requests**.
    

---

## **Installing `ffuf`**

To install `ffuf` on **Linux** (Kali, Ubuntu) or **macOS**:

```bash
sudo apt install ffuf  # Debian-based systems (Kali, Ubuntu)
brew install ffuf      # macOS (Homebrew)
```

Alternatively, you can download and compile it from source:

```bash
git clone https://github.com/ffuf/ffuf.git
cd ffuf
go get
go build
```

---

## **Basic Usage of `ffuf`**

`ffuf` works by **brute-forcing** a given input (e.g., directory names, parameters, or subdomains) against a target.

### **1. Directory Fuzzing**

This method is used to find **hidden files and directories** on a web server.

```bash
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

 **Explanation**:

- `-u http://target.com/FUZZ` → **Target URL** where `FUZZ` is the **placeholder** to be replaced by each word in the wordlist.
    
- `-w /usr/share/wordlists/dirb/common.txt` → **Wordlist** containing common directory names.
    

 **Example Output**:

```
/admin            [Status: 200, Size: 1234]
/login            [Status: 200, Size: 1024]
/backup           [Status: 403, Size: 512]
```

 **Useful Options**:

- `-fc 403` → **Filter out** responses with status code **403** (Forbidden).
    
- `-mc 200` → **Only show results** with status **200 OK**.
    

---

### **2. Finding Hidden Files**

We can search for **hidden files** like `.php`, `.bak`, `.zip` using extensions.

```bash
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php,.bak,.zip
```

 **Explanation**:

- `-e .php,.bak,.zip` → Adds **file extensions** to each word in the list.
    

 **Example Output**:

```
/config.php       [Status: 200, Size: 1536]
/backup.zip       [Status: 200, Size: 5120]
```

---

### **3. Subdomain Enumeration**

Used to find **subdomains** of a target.

```bash
ffuf -u http://FUZZ.target.com -w /usr/share/wordlists/dns/subdomains-top1million-5000.txt -H "Host: FUZZ.target.com"
```

 **Explanation**:

- `FUZZ.target.com` → The `FUZZ` placeholder will be replaced with subdomains from the wordlist.
    
- `-H "Host: FUZZ.target.com"` → Adds a custom **Host header**, useful when testing virtual hosts.
    

 **Example Output**:

```
admin.target.com       [Status: 200, Size: 2048]
beta.target.com        [Status: 200, Size: 1024]
```

---

### **4. Parameter Discovery (GET & POST)**

To find **hidden GET parameters**:

```bash
ffuf -u "http://target.com/page.php?FUZZ=test" -w /usr/share/wordlists/parameters.txt
```

 **Example Output**:

```
id             [Status: 200, Size: 1234]
debug          [Status: 200, Size: 512]
```

Now, we know `id` and `debug` are valid parameters.

---

### **5. Fuzzing POST Requests**

To test for **hidden POST parameters**:

```bash
ffuf -u "http://target.com/login" -X POST -w /usr/share/wordlists/parameters.txt -d "FUZZ=admin&password=123"
```

 **Explanation**:

- `-X POST` → Uses **POST method**.
    
- `-d "FUZZ=admin&password=123"` → Fuzzes the **parameter name** in a POST request.
    

 **Example Output**:

```
username        [Status: 200, Size: 1536]
email           [Status: 200, Size: 1024]
```

Now, we know the app is accepting **username** and **email** as valid parameters.

---

### **6. Bypassing WAF/403 Forbidden**

Sometimes, a **firewall (WAF) blocks direct scanning**. We can **bypass WAF** using:

```bash
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -H "X-Forwarded-For: 127.0.0.1"
```

- `-H "X-Forwarded-For: 127.0.0.1"` → Tricks the server into thinking the request is from localhost.
    

Other bypass techniques:

- **Change User-Agent**: `-H "User-Agent: Googlebot"`
    
- **Use random delays**: `-p 0.1-0.5` (random delays between requests).
    

---

## **Advanced Usage**

### **7. Recursive Directory Fuzzing**

To **automatically fuzz discovered directories**, use:

```bash
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -recursion
```

 If `/admin/` is found, `ffuf` will **automatically** start fuzzing inside `/admin/`.

---

### **8. Filtering & Matching**

You can **filter results** based on:

- Status Code (`-fc`): `-fc 403` → Filter **403 Forbidden** responses.
    
- Response Size (`-fs`): `-fs 0` → Ignore responses with **0 bytes**.
    
- Response Words (`-fw`): `-fw 10` → Ignore responses with exactly **10 words**.
    

Example:

```bash
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -fc 403 -fs 0
```

 **This filters out 403 errors and empty responses**.

---

## **When to Use `ffuf`?**

|Scenario|Command Example|
|---|---|
|**Find hidden directories**|`ffuf -u http://target.com/FUZZ -w common.txt`|
|**Find hidden files**|`ffuf -u http://target.com/FUZZ -w common.txt -e .php,.bak`|
|**Find subdomains**|`ffuf -u http://FUZZ.target.com -w subdomains.txt`|
|**Find GET parameters**|`ffuf -u "http://target.com/page.php?FUZZ=test" -w params.txt`|
|**Fuzz POST parameters**|`ffuf -u "http://target.com/login" -X POST -d "FUZZ=admin&password=123" -w params.txt`|
|**Bypass WAF**|`ffuf -u http://target.com/FUZZ -w common.txt -H "X-Forwarded-For: 127.0.0.1"`|
