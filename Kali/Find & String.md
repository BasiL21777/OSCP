# Linux Command Notes: find & strings

## `find` — search files and directories

**Basic syntax:**

```bash
find <path> <conditions> <actions>
```

**Important options:**

- **`-type f`** → files only
    
- **`-type d`** → directories only
    
- **`-name "<pattern>"`** → match name (supports wildcards)
    
- **`-iname "<pattern>"`** → case-insensitive name match
    
- **`-size <n>`** → file size exactly `n`
    
- **`-size +<n>`** → larger than `n`
    
- **`-size -<n>`** → smaller than `n`
    
- **`-exec <command> {} \;`** → run a command on each result
    
- **`-maxdepth <n>`** → limit recursion depth
    
- **`-mindepth <n>`** → skip top levels
    
- **`-perm <mode>`** → match file permissions
    

**Examples:**

```bash
# Find all files smaller than 1 KB
find . -type f -size -1k

# Find all ASCII text files
find . -type f -exec file {} \; | grep ASCII

# Find all *.txt files case-insensitive
find /home/user -type f -iname "*.txt"

# Run cat on all files smaller than 1 KB
find . -type f -size -1k -exec cat {} \;
```

---

## `strings` — extract readable text from binary files

**Basic syntax:**

```bash
strings [options] <file>
```

**Important options:**

- **`-a`** → scan the whole file (not just data segment)
    
- **`-n <number>`** → minimum string length (default 4)
    
- **`-t <format>`** → show string offsets (`x` = hex, `d` = decimal, `o` = octal)
    
- **`-e <encoding>`** → specify encoding (`s`=single-byte, `b`=16-bit BE, `l`=16-bit LE)
    

**Examples:**

```bash
# Show all readable strings in a file
strings file.bin

# Show strings with minimum length of 6
strings -n 6 file.bin

# Scan entire file (including binaries)
strings -a file.bin
```

---

### Notes for Pentesting / CTF

- Use `find` to locate:
    
    - hidden files (`-name ".*"`)
        
    - files of specific size (`-size`)
        
    - files with specific permissions (`-perm`)
        
- Use `strings` to:
    
    - extract passwords or keys from binaries
        
    - inspect unusual files when `cat` breaks terminal
        
- Combine `find` + `file` + `strings` for automated reconnaissance:
    

```bash
find . -type f -exec file {} \; | grep ASCII
find . -type f -size -1k -exec strings {} \;
```
