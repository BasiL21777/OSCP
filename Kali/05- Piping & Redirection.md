#kali
## **Lesson #2: Piping & Redirection**

1. **Understanding Input/Output Streams:**
    
    - Every command works with **input** (0) and **output** streams:
        
        - `1>` = **Standard Output** (valid output)
            
        - `2>` = **Standard Error** (error messages)
            
2. **Redirection Basics:**
    
    - `echo "Hello" > hello.txt`
        
        - Redirects the output of `echo` to a file (overwrites if exists).
            
    - `>>` Appends to a file instead of overwriting.
        
        - `echo "World" >> hello.txt`
            
    - `<` Used for redirecting **input** from a file.
        
        - `a=file`
            
        - `cat < $a` – Reads content from `file` and displays it.
            
    - Example of redirecting output and error:
        
        - `ls .. a 1>parentDir 2>error`
            
        - Saves standard output in `parentDir`, errors in `error`.
            

---

3. **Piping:**
    
    - Sends the **output of one command** as **input to another** using `|`.
        
        - `cat file | wc` – Sends content of `file` to `wc`.
            

---

4. **Using `tee`:**
    
    - Displays output and **saves it to a file** at the same time.
        
        - `echo "Hello" | tee hello.txt`
            

---

5. **Using `xargs`:**
    
    - Passes **input as arguments** to a command.
        
    - Example:
        
        - `ls | rm` →  won't work (missing arguments for `rm`)
            
        - `ls | xargs rm` →  deletes listed files
            
    - Count lines of multiple files:
        
        - `ls | xargs wc` – Counts lines in each file
            
        - `ls | wc` – Counts number of lines in `ls` output itself (not files)
            

---
### **[[06- Manage Process|Next]]**
