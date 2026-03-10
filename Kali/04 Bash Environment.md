#kali
## 🧠 **Lesson: Bash Environment**

1. **Variables in Bash:**
    
    - `a="basil"` – Define a **temporary variable**.
        
    - `echo $a` – Print the value of variable `a`.
        
    - By default, variables are **session-based** and only available in the terminal where they are defined.
        
    - Opening a new shell (e.g., typing `bash`) won't retain these variables:
        
        - `bash`
            
        - `echo $a` – Will return nothing.
            
2. **Making Variables Global (for current session):**
    
    - `export a="bassel"` – Make variable **available in subshells**.
        
    - This is still **temporary** — it resets on logout or reboot.
        
3. **Viewing All Environment Variables:**
    
    - `env` – Show all environment variables.
        
    - These include `PATH`, `HOME`, `USER`, and more.
        
4. **Understanding `$PATH`:**
    
    - `echo $PATH` – Show system paths where commands are searched.
        
    - Paths are separated by colons (`:`).
        
    - If you type a command not found in these paths (e.g., `akshd`), you'll get:  
        `command not found`
        
5. **Temporarily Making a Script Globally Accessible:**
    
    - Example steps:
        
        1. `nano myscript` – Write your script.
            
        2. `chmod +x myscript` – Make it executable.
            
        3. `export PATH=/path/to/myscript_dir:$PATH` – Add your directory to the front of `$PATH`.
            
    - Now you can run `myscript` from anywhere.
        
    - ⚠️ This change is **temporary** — it disappears after logout.
        
6. **Permanently Adding Scripts to PATH:**
    
    - Move your script to a system path:
        
       - `sudo mv myscript /usr/bin`
            
    - Now the script is available across all sessions and users.
        
7. **Danger Zone: `unset PATH`:**
    
    - `unset PATH` – Deletes the `$PATH` variable.
        
    - After that, common commands like `ls`, `env`, or `sudo` won't work.
        
    - You must use full paths:
        
        - `/bin/ls`, `/usr/bin/env`
            
8. **Security Risk Example – Path Hijacking:**
    
    - A malicious attacker could trick you into executing bad code:
        
        1. `nano sudo` – Write a fake version of the `sudo` command.
            
        2. `chmod +x sudo`
            
        3. `export PATH=/path/to/fake_sudo:$PATH`
            
        4. Now `sudo apt update` will run the **fake script**, not the real one.
            
    - This only affects the **current session** unless made permanent in `.bashrc`.
9.  Add Alias Permanent:
	1. `nano  ~/.bashrc` 
		* or .zshrc  => in case u use zsh 
	2. `source ~/.bashrc`
	
---
## **Bash History & Command Execution**

1. **Command History:**
    
    - `history` – Shows all commands you've run in the current session.
        
    - `!50` – Re-executes the command at line **50** from history.
        
    - Bash stores command history in:
        
        - `~/.bash_history`
            
2. **Chaining Commands:**
    
    - `ls && cat /etc/passwd`
        
        - Runs `cat /etc/passwd` **only if** `ls` executes successfully.
            
        - `&&` means: **execute next command only if the previous one succeeds**.
            
    - `ls ; cat /etc/passwd`
        
        - Runs `cat /etc/passwd` **regardless** of whether `ls` succeeds or fails.
            
        - `;` means: **run the next command unconditionally**.
            
