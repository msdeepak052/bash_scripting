# **`for` loop** in bash script

In Bash scripting, the **`for` loop** is a powerful construct used to iterate over a sequence of items or execute a block of code repeatedly. There are **two major types** of `for` loops in Bash:

---

## 🔁 1. **List-Based `for` Loop (most common)**

This loop is used to iterate over a **list of items**, such as strings, numbers, or output of a command.

### 🔹 Syntax:

```bash
for var in list
do
  # commands using $var
done
```

### 🔹 Example 1: Loop through filenames

```bash
for file in file1.txt file2.txt file3.txt
do
  echo "Processing $file"
done
```

### 🔹 Example 2: Loop through a sequence of numbers

```bash
for i in 1 2 3 4 5
do
  echo "Number: $i"
done
```

### 🔹 Example 3: Using command substitution

```bash
for user in $(cut -d: -f1 /etc/passwd)
do
  echo "User: $user"
done
```

---

## 🧮 2. **C-Style `for` Loop (like C, Java, etc.)**

This loop resembles the traditional C-style syntax, useful when working with numeric ranges and conditions.

### 🔹 Syntax:

```bash
for (( initialization; condition; increment ))
do
  # commands
done
```

### 🔹 Example 1: Print numbers 1 to 5

```bash
for (( i=1; i<=5; i++ ))
do
  echo "Counter: $i"
done
```

### 🔹 Example 2: Countdown

```bash
for (( i=10; i>=1; i-- ))
do
  echo "Countdown: $i"
done
```

---

## ✅ Real-World Use Cases

### 🛠️ Case 1: Backing up files

```bash
for file in *.log
do
  cp "$file" "$file.bak"
  echo "Backed up $file"
done
```

### 🧪 Case 2: Pinging a list of servers

```bash
for server in google.com yahoo.com example.com
do
  ping -c 1 $server > /dev/null
  if [ $? -eq 0 ]; then
    echo "$server is reachable"
  else
    echo "$server is NOT reachable"
  fi
done
```

### 💡 Case 3: Retry loop with C-style

```bash
for (( attempt=1; attempt<=3; attempt++ ))
do
  echo "Attempt $attempt to connect..."
  curl -s http://example.com && break
  sleep 2
done
```

---

## 📌 Key Notes

| Feature     | List-Based `for`                               | C-Style `for`                |
| ----------- | ---------------------------------------------- | ---------------------------- |
| Input       | List of values (strings, files, numbers, etc.) | Numbers with condition       |
| Use case    | Iterating files, strings, command output       | Counting, looping with logic |
| Flexibility | Easier for non-numeric iteration               | Good for numeric iteration   |

---

# **`while` loop** in bash script


## 🔁 `while` Loop in Bash

The `while` loop repeatedly executes a block of code **as long as a condition is true**. It is ideal when you don’t know how many times you’ll loop — unlike `for` which is often used with known lists or ranges.

---

## 📌 Syntax:

```bash
while [ condition ]
do
  # commands
done
```

You can also use `(( ))` for arithmetic conditions or any command (e.g., `read`, `ping`, etc.) directly.

---

## 🔹 Example 1: Simple Counter

```bash
#!/bin/bash
counter=1
while [ $counter -le 5 ]
do
  echo "Counter: $counter"
  ((counter++))
done
```

---

## 🔹 Example 2: Reading user input until a condition

```bash
#!/bin/bash
while true
do
  read -p "Enter 'yes' to proceed: " input
  if [ "$input" == "yes" ]; then
    echo "Proceeding..."
    break
  fi
done
```

---

## 🔹 Example 3: Using command as a condition

```bash
#!/bin/bash
while ping -c1 google.com &> /dev/null
do
  echo "Internet is up. Checking again in 5 seconds..."
  sleep 5
done
```

---

## 🔹 Example 4: Reading a file line by line

```bash
#!/bin/bash
while IFS= read -r line
do
  echo "Line: $line"
done < myfile.txt
```

---

## 🔹 Example 5: Countdown using `while`

```bash
#!/bin/bash
count=10
while [ $count -gt 0 ]
do
  echo "Countdown: $count"
  ((count--))
  sleep 1
done
```

---

## ✅ Real-World Use Cases

### 🧪 1. Retry a command until success or timeout

```bash
attempts=0
while ! curl -s https://example.com && [ $attempts -lt 5 ]
do
  echo "Retrying in 3 seconds..."
  ((attempts++))
  sleep 3
done
```

---

### 📂 2. Archive old files

```bash
#!/bin/bash
while read -r file
do
  gzip "$file"
  echo "Archived $file"
done < <(find /var/log -name "*.log" -mtime +7)
```

---

### 👥 3. Wait for a user to login (simulate)

```bash
#!/bin/bash
while ! who | grep -q "deepak"
do
  echo "Waiting for user deepak to login..."
  sleep 10
done
echo "User deepak has logged in."
```

---

## 🧠 Key Takeaways

| Feature          | `while` Loop                                     |
| ---------------- | ------------------------------------------------ |
| Loop type        | Conditional (runs as long as condition is true)  |
| Best for         | Unknown number of iterations                     |
| Common use cases | User input, file reading, waiting on services    |
| Variants         | `until` loop (runs until condition becomes true) |

---

# `until` loop** in Bash scripting

---

## 🔁 `until` Loop in Bash

The `until` loop is the **opposite** of the `while` loop.

* It **executes commands repeatedly *until* the condition becomes true**.
* In other words, it **runs while the condition is false**, and **stops when the condition is true**.

---

## 📌 Syntax:

```bash
until [ condition ]
do
  # commands
done
```

> The block executes **as long as the condition is false**. Once the condition becomes true, the loop stops.

---

## 🔹 Example 1: Simple counter using `until`

```bash
#!/bin/bash
count=1
until [ $count -gt 5 ]
do
  echo "Count is $count"
  ((count++))
done
```

🔸 Runs when `$count <= 5`, stops when `$count > 5`.

---

## 🔹 Example 2: Waiting for a file to exist

```bash
#!/bin/bash
until [ -f /tmp/ready.flag ]
do
  echo "Waiting for /tmp/ready.flag to be created..."
  sleep 2
done
echo "File found!"
```

---

## 🔹 Example 3: Wait for a service to stop

```bash
#!/bin/bash
until ! systemctl is-active --quiet myservice
do
  echo "Waiting for myservice to stop..."
  sleep 3
done
echo "Service has stopped."
```

---

## 🔹 Example 4: Run until valid input is entered

```bash
#!/bin/bash
until [[ $name =~ ^[A-Za-z]+$ ]]
do
  read -p "Enter your name (letters only): " name
done
echo "Hello, $name!"
```

---

## 🔹 Example 5: Until website is reachable (inverted `while`)

```bash
#!/bin/bash
until curl -s --head http://example.com | grep "200 OK" > /dev/null
do
  echo "Waiting for example.com to become available..."
  sleep 2
done
echo "Website is live!"
```

---

## ✅ Real-World Use Cases

### 🛠️ 1. Polling a remote resource until it's available

```bash
until curl -s https://api.server.com/health | grep '"status":"ok"' > /dev/null
do
  echo "Waiting for server health to be OK..."
  sleep 5
done
echo "Server is healthy."
```

---

### 🔄 2. Retry uploading a file until it succeeds

```bash
until scp file.txt user@server:/path/
do
  echo "Upload failed, retrying in 10 seconds..."
  sleep 10
done
echo "Upload successful!"
```

---

## 🧠 Comparison: `while` vs `until`

| Feature         | `while` Loop                     | `until` Loop                       |
| --------------- | -------------------------------- | ---------------------------------- |
| Condition logic | Runs **while** condition is true | Runs **until** condition is true   |
| Stops when      | Condition becomes false          | Condition becomes true             |
| Common use      | Repeating on success/valid state | Waiting for failure or final state |
| Inverted logic  | No                               | Yes (opposite logic)               |

---

## 📦 Summary

* Use `while` for loops **based on continuing success**.
* Use `until` for loops **based on eventual success after failure** (e.g., waiting for file/service/API readiness).
* Both loops are flexible, depending on how your logic is phrased.

---

# **`break` and `continue`** 

---

## 🔄 What are `break` and `continue` in Bash?

They are **loop control statements** used inside `for`, `while`, or `until` loops.

| Command    | Description                                                    |
| ---------- | -------------------------------------------------------------- |
| `break`    | Immediately exits the **entire loop** (no further iterations). |
| `continue` | Skips the **current iteration** and moves to the next one.     |

---

## 🛑 `break` Statement

### 🔹 Syntax:

```bash
break
```

### 🔹 Example 1: Stop when a match is found

```bash
for num in 1 2 3 4 5
do
  if [ $num -eq 3 ]; then
    echo "Found 3, breaking the loop"
    break
  fi
  echo "Number: $num"
done
```

**Output:**

```
Number: 1
Number: 2
Found 3, breaking the loop
```

---

### 🔹 Example 2: Exit a `while` loop on condition

```bash
count=1
while true
do
  echo "Count: $count"
  ((count++))
  if [ $count -gt 3 ]; then
    break
  fi
done
```

---

## ⏭️ `continue` Statement

### 🔹 Syntax:

```bash
continue
```

### 🔹 Example 1: Skip even numbers

```bash
for num in {1..5}
do
  if (( num % 2 == 0 )); then
    continue
  fi
  echo "Odd number: $num"
done
```

**Output:**

```
Odd number: 1
Odd number: 3
Odd number: 5
```

---

### 🔹 Example 2: Skip blank lines in a file

```bash
while IFS= read -r line
do
  [[ -z "$line" ]] && continue
  echo "Line: $line"
done < input.txt
```

---

## ✅ Real-World Use Cases

### 💡 Use of `break` in search

```bash
for user in $(cut -d: -f1 /etc/passwd)
do
  if [ "$user" == "deepak" ]; then
    echo "User deepak found"
    break
  fi
done
```

---

### ⚙️ Use of `continue` in file filtering

```bash
for file in *.log
do
  [[ $file == *error* ]] && continue
  echo "Processing $file"
done
```

---

## 🧠 `break` and `continue` with nested loops

```bash
for i in 1 2 3
do
  for j in a b c
  do
    if [[ $j == "b" ]]; then
      break 2  # break out of both loops
    fi
    echo "$i - $j"
  done
done
```

---

## 📦 Summary

| Command    | Purpose                                  | Exits Loop? | Skips Iteration? |
| ---------- | ---------------------------------------- | ----------- | ---------------- |
| `break`    | Stop entire loop when a condition is met | ✅ Yes       | ❌ No             |
| `continue` | Skip current iteration and move to next  | ❌ No        | ✅ Yes            |

---

# **loop over files, command output, and arrays** in Bash scripting 

---

## 🔁 1. **Looping Over Files**

### 🔹 a. Using `for` with globbing

```bash
for file in *.txt
do
  echo "File: $file"
done
```

✅ **Use case**: List or process all `.txt` files in a directory.

---

### 🔹 b. Using `find` (safer with large or recursive directories)

```bash
find /path/to/dir -type f -name "*.log" | while read -r file
do
  echo "Found file: $file"
done
```

✅ **Use case**: Scan logs in subdirectories.

---

### 🔹 c. Loop over files line by line

```bash
while IFS= read -r file
do
  echo "Line (filename): $file"
done < filelist.txt
```

✅ **Use case**: Reading a list of filenames from a file.

---

## 🧾 2. **Looping Over Command Output**

### 🔹 a. Using command substitution in `for` loop

```bash
for user in $(cut -d: -f1 /etc/passwd)
do
  echo "User: $user"
done
```

❗ *Warning*: This splits on spaces/tabs — problematic for filenames or values with spaces.

---

### 🔹 b. Safer: Use `while` with pipe

```bash
cut -d: -f1 /etc/passwd | while read -r user
do
  echo "User: $user"
done
```

✅ **Use case**: More reliable for processing space-containing output (e.g., logs, usernames, paths).

---

## 📚 3. **Looping Over Arrays**

### 🔹 a. Declaring and iterating arrays

```bash
fruits=("apple" "banana" "cherry")
for fruit in "${fruits[@]}"
do
  echo "Fruit: $fruit"
done
```

✅ **Best practice**: Always quote `"${array[@]}"` to preserve values with spaces.

---

### 🔹 b. Loop using index

```bash
for (( i=0; i<${#fruits[@]}; i++ ))
do
  echo "Fruit $i: ${fruits[$i]}"
done
```

✅ **Use case**: When index is needed or partial array iteration is desired.

---

### 🔹 c. Adding items dynamically

```bash
myarr=()
myarr+=("item1")
myarr+=("item2")

for item in "${myarr[@]}"
do
  echo "$item"
done
```

---

## ✅ Real-World Examples

### 🛠️ 1. Process files modified in the last 1 day

```bash
find . -type f -mtime -1 | while read -r file
do
  echo "Recently modified: $file"
done
```

---

### 💬 2. Check which services are active

```bash
for service in nginx docker sshd
do
  systemctl is-active --quiet $service && echo "$service is running"
done
```

---

### 📦 3. Loop over running processes (filtered)

```bash
ps aux | grep nginx | while read -r line
do
  echo "$line"
done
```

---

### 📁 4. Batch rename files with array

```bash
files=( *.txt )
for file in "${files[@]}"
do
  mv "$file" "${file%.txt}.bak"
  echo "Renamed $file"
done
```

---

## 🧠 Summary Table

| Loop Type                 | Best For                             | Safe for spaces? |
| ------------------------- | ------------------------------------ | ---------------- |
| `for file in *`           | Simple file listing                  | ❌ (use quotes)   |
| `while read`              | Reading lines/command output         | ✅                |
| `for item in $(cmd)`      | Quick looping through command output | ❌                |
| `for item in "${arr[@]}"` | Looping arrays safely                | ✅                |

---




