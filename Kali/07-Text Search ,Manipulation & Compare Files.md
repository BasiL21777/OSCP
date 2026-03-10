#kali
##  **#3 Text Search and Manipulation:**

###  **`grep` – Search in files or outputs**

```bash
grep "pattern" file
```

- `-i` → Ignore case sensitivity
    
- `-v` → Invert match (show lines **not** matching)
    
- `-r` → Recursively search in all files in a directory
    

 **Examples:**

```bash
grep hello file.txt
cat file.txt | grep hello -v   # show lines without 'hello'
cat file | grep -i flag        # search case-insensitive for 'flag'
grep "pass\|admin" file        # search for 'pass' OR 'admin'
```

---

 **Regular Expressions in `grep`:**

| Pattern  | Meaning                                |
| -------- | -------------------------------------- |
| `.`      | Any single character                   |
| `*`      | Zero or more of the previous character |
| `^`      | Beginning of line                      |
| `$`      | End of line                            |
| `[abc]`  | Match a, b, or c                       |
| `[^abc]` | Match anything **except** a, b, or c   |
| `\|`     | OR operator                            |

 Example:

```bash
grep "^root" /etc/passwd       # lines starting with root
grep "admin$" users.txt        # lines ending with admin
grep "[0-9]" file.txt          # lines with any digit
```

---

🧪 **`sed` – Stream Editor (edit without opening file)**

```bash
sed "s/old/new/g" file
```

- `s` → substitute
    
- `g` → global (replace all matches in line)
    

 Example:

```bash
sed "s/password/admin/g" file.txt
```

 **In-place editing:**

```bash
sed -i "s/password/admin/g" file.txt
```

---

 **`split` – Split large files (useful in brute force)**

```bash
split -l 1000 file new_
```

- `-l` → number of lines per new file
    
- Creates files: `new_aa`, `new_ab`, ...
    

---

 **`cut` & `awk` – Column manipulation**

###  `cut`

```bash
cut -d ":" -f 1,6,7 /etc/passwd
```

- `-d` → delimiter
    
- `-f` → fields/columns to extract
    

---

###  `awk` – More powerful text processor

```bash
awk -F ":" '{ print $1, $6, $7 }' /etc/passwd
```

- `-F` → field separator (like `-d` in cut)
    
- `$1`, `$2`, ... → column variables
    
- Can use conditions and logic (like if/else)
    

Example:

```bash
awk '{ if ($3 > 1000) print $1 }' /etc/passwd
```

---

 **Practical Example: Analyze Logs**

```bash
cat apache_logs | cut -d " " -f 1 | uniq -c | sort
```

1. Extract 1st column (IP addresses)
    
2. `uniq -c` → Count unique IPs
    
3. `sort` → Sort by frequency
    


---

##  **4 Compare Files**

###  **`comm` – Compare Two Sorted Files**

```bash
comm file1 file2
```

- Compares **two sorted files line by line**
    
- Output has **three columns**:
    

|Column|Description|
|---|---|
|1|Lines **only in `file1`**|
|2|Lines **only in `file2`**|
|3|Lines in **both files**|

Example:

```bash
comm f1.txt f2.txt
```

 **Files must be sorted**. Use:

```bash
sort f1.txt -o f1.txt
```

---

###  **`diff` – Show Differences Line by Line**

```bash
diff file1 file2
```

- Compares files **line by line**
    
- Shows **what needs to change** in `file1` to make it identical to `file2`
    

###  Example Output:

```
3c3
< Hello world
---
> Hello World!
```

 **Explanation**:

- Line 3 is different:
    
    - `<` means from `file1`
        
    - `>` means from `file2`
        
    - `c` means "change"
        

---

### Other useful `diff` options:

|Option|Description|
|---|---|
|`-y`|Side-by-side comparison|
|`--suppress-common-lines`|Hide matching lines in `-y` mode|
|`-i`|Ignore case|
|`-B`|Ignore blank lines|
|`-r`|Compare directories recursively|

 Example:

```bash
diff -y file1.txt file2.txt
```

---
### **[[08 File and Command Monitoring|Next]]**
