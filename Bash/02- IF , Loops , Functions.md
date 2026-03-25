##  Bash Scripting – Lesson 3: `if`, `else`, `elif`, Loops, and Functions

---

###  `if`, `else`, `elif` Statements

####  Syntax:

```bash
#!/bin/bash

grade=85

if [ "$grade" -gt 90 ]; then
    echo "Grade: A"
elif [ "$grade" -gt 80 ]; then
    echo "Grade: B"
else
    echo "Grade: C"
fi
```

>  **Use `-gt` instead of `>`** for numeric comparison in Bash. Always quote variables (`"$grade"`) to avoid issues with empty values.

####  Numeric comparison operators:

|Operator|Meaning|
|---|---|
|`-eq`|equal|
|`-ne`|not equal|
|`-gt`|greater than|
|`-lt`|less than|
|`-ge`|greater or equal|
|`-le`|less or equal|

---

###  Logical Operators

|Operator|Meaning|
|---|---|
|`!`|NOT|
|`&&` / `-a`|AND|
|`||

####  Example:

```bash
if [ "$grade" -gt 80 ] && [ "$grade" -lt 90 ]; then
    echo "B grade range"
fi
```

---

###  Loops in Bash

####  `for` Loop

```bash
for i in 1 2 6 8; do
    echo "Value: $i"
done
```

####  Using `seq`:

```bash
for i in $(seq 1 10); do
    echo "num: $i"
done
```

####  Using brace expansion:

```bash
for i in {1..10}; do
    echo "num: $i"
done
```

####  Full Example:

```bash
#!/bin/bash

for i in {1..5}; do
    echo "Number: $i"
done
```

---

###  `while` Loop

```bash
#!/bin/bash

i=0
while [ $i -lt 5 ]; do
    echo "num: $i"
    ((i++))  # Arithmetic operation
done
```

---

###  Functions in Bash

####  Basic Function Example

```bash
#!/bin/bash

greet() {
    echo "Hi $1"
}

greet "$1"
```

>  Run the script with a name:

```bash
./script.sh Bassel
```

---

###  Bonus Tips:

- You **must define the function before calling it** in Bash.
    
- Function parameters are passed like script arguments: `$1`, `$2`, etc.
    
- Use `return` to exit early or return a numeric status.
    

---
### [[03- Exercise 1|Next]]
