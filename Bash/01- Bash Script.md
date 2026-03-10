## 🧠 Bash Scripting : Introduction

---

### 📌 What is Bash?

1. **Bash** is a _shell environment_ — a command-line interpreter like Python or PowerShell.
    
2. We use Bash to **automate tasks** and execute sequences of commands.
    
3. Every Bash script should start with:
    
    ```bash
    #!/bin/bash
    ```
    
    This is called a **shebang**, telling the OS to run the script using the Bash interpreter.
    

---

### 🧾 File Execution Rules

You can run Bash scripts in multiple ways:

|Method|Description|
|---|---|
|`bash file.sh`|Runs the script without making it executable|
|`./file.sh`|Requires executable permissions (`chmod +x file.sh`)|
|`#!/bin/bash` in the script|Tells OS this is a Bash script|
|`.sh` file extension|Common convention, but not required|

> 🧠 `#!/bin/python` would make it run using Python instead.

---

### 🔑 Make Script Executable

```bash
chmod +x file.sh
```

---

### 🔄 Command Substitution

Used to assign command output to a variable or insert into strings.

```bash
V=$(date)
echo "Date is: $V"

# OR using backticks (old method)
echo "Date is: `date`"
```

---

### 🧮 Script Arguments and Special Variables

|Symbol|Description|
|---|---|
|`$0`|The name of the script file|
|`$1`, `$2`, ..., `$n`|Positional arguments passed to the script|
|`$#`|Number of arguments passed|
|`$*`|All arguments as a **single string**|
|`$@`|All arguments as **separate words**|
|`$$`|PID (Process ID) of the current script|
|`$?`|Exit status of the last command (0 = success)|
|`$!`|PID of the last background process|

---

### 🧪 Example 1: Variables and Substitution

```bash
#!/bin/bash
A="Bassel"
B="Yasser"
C="will unset"

unset -v C  # Removes C

echo "Welcome $A $B $C"

# Command substitution
V=$(date)
echo "Date (method 1): $V"
echo "Date (method 2): `date`"

# Script arguments
echo "arg0: $0, arg1: $1, arg2: $2"
```

#### 💡 Run Example:

```bash
./file.sh Bassel 21
```

---

### 🧪 Example 2:  Process Testing

``` bash
#!/bin/bash
echo "Hello from process $$"
sleep 20
kill -9 $$
echo "This will never print"
```

#### 🔍 Monitor with:

```bash
watch -n 0.5 -d "ps aux | grep sleep"
```

This shows the running `sleep` command and helps you observe the process before it gets killed.

---
