#kali
## 🧠 **Lesson #5: Managing Processes**

1. **Foreground Processes:**
    
    - When running tools like `nmap`, the terminal is **blocked** until the command finishes.
        
    - Example:
        
        ```bash
        sleep 9000
        ```
        
        You can't use the terminal until it's done or you stop it.
        

---

2. **Background Processes (`&`):**
    
    - Add `&` at the end of a command to run it in the background:
        
        ```bash
        sleep 20 &
        ```
        
        - The shell will return a **job ID** and a **PID** (Process ID).
            
        - You get control of the terminal back immediately.
            

---

3. **View and Manage Jobs:**
    
    - `jobs` – Shows background or stopped jobs:
        
        - `+` = most recent
            
        - `-` = second most recent
            
    - `fg` – Bring a background job to the **foreground**:
        
        - `fg` – brings the `+` job.
            
        - `fg %2` – brings job with ID 2.
            
    - `bg` – Resume a **stopped** job in the **background**:
        
        - `bg` – resumes last stopped job.
            
        - `bg %2` – resumes job with ID 2.
            
    - Stopping a foreground job:
        
        - `Ctrl+Z` – **Pauses** the process (can be resumed later).
            
        - `Ctrl+C` – **Terminates** the process immediately.
            

---

4. **Process List:**
    
    - `ps` – Shows current processes in this terminal.
        
    - `ps aux` – Shows **all** running processes (like Task Manager).
        
    - `ps aux | grep sleep` – Filter to find specific process.
        

---

5. **Keeping Jobs Alive After Terminal Closes:**
    
    - By default, background jobs **end** when you close the terminal — because of a `SIGHUP` (hangup) signal.
        
    - To prevent this, use `nohup`:
        
        ```bash
        nohup sleep 9000 &
        ```
        
        - Ignores the hangup signal, so process keeps running even after terminal closes.
            
        - Output is usually redirected to `nohup.out` by default.
            

---

6. **If You Forgot to Use `nohup`:**
    
    - You can prevent the job from ending by **detaching** it:
        
        ```bash
        disown
        disown %3
        ```
        
        - Removes the job from the shell's job table, so it won’t receive `SIGHUP`.
            

---

7. **Limitation of `nohup`:**
    
    - When you restart the terminal, the process still runs, **but you can’t control it** using `jobs`, `fg`, or `bg`.
        

---

8. **Solution: Use `screen` or `tmux`:**
    
    ✅ These are terminal multiplexer tools that let you:
    
    - Run long processes in **detachable sessions**.
        
    - **Detach** from the session, close the terminal, then **reattach** later.
        
    - Regain full control of processes at any time.
        
    
    Example using `screen`:
    
    ```bash
    screen  # Start a new session
	screen -S session_name   # Start a new named session
    Ctrl+A then D  # Detach
    screen -ls      # List sessions
    screen -r       # Reattach session
    screen -r session_name #Reattach to a specific session
    exit or Ctr+D  #exit session
    
    ```


------

## 🧠 **Lesson: Linux Signals & Killing Processes**

### 🔫 Sending Signals to Processes:

```bash
kill -[signal] PID
```

- Signals are used to **communicate with processes** — to stop, interrupt, hang up, or force kill them.
    

---

### 🧱 Common Signal Types:

|Signal|Command|Meaning|
|---|---|---|
|`-1`|`kill -1 PID`|**SIGHUP** – Hangup (terminal closed)|
|`-2`|`kill -2 PID`|**SIGINT** – Interrupt (like `Ctrl+C`)|
|`-15`|`kill -15 PID`|**SIGTERM** – Graceful termination (default)|
|_(none)_|`kill PID`|Same as `kill -15`|
|`-9`|`kill -9 PID`|**SIGKILL** – Force kill (cannot be ignored)|

---

### 💥 When to Use Which Signal?

- `-15` (default): Safest, allows the process to clean up.
    
- `-9`: Use only when a process **won’t die** or is **hanging**.
    
- `-2`: Simulates `Ctrl+C`, often used in scripts.
    
- `-1`: Used to restart processes after config changes (e.g. daemons).
    

---

### 🔄 Killing Multiple Processes (same name):

- If many processes have the **same name** (e.g., `sleep`), you **can’t loop by PID**, since they're non-sequential.
    
- Use:
    
    ```bash
    killall sleep
    ```
    
    - Sends `SIGTERM` by default (like `kill -15`)
        
    - You can specify a signal:
        
        ```bash
        killall -9 sleep
        killall -2 sleep
        ```
        

✅ Make sure the **name is correct** — use `ps aux | grep sleep` to check.
