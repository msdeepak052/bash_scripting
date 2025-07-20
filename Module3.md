# Coditional Statements in Bash

In **Bash scripting**, conditional statements are used to make decisions and execute different blocks of code based on certain conditions. The main conditional statements in Bash are:

---

### 🔹 1. `if` Statement

#### **Syntax**:

```bash
if [ condition ]; then
    # commands
fi
```

#### ✅ **Example**:

```bash
#!/bin/bash

count=10

if (( count > 5 )); then
    echo "Count is greater than 5"
fi
```

#### 🧠 **Use Case**:

Used when you want to run a block of code only **if a condition is true**.

---

### 🔹 2. `if-else` Statement

#### **Syntax**:

```bash
if [ condition ]; then
    # commands if true
else
    # commands if false
fi
```

#### ✅ **Example**:

```bash
#!/bin/bash

name="Deepak"

if [ "$name" == "Deepak" ]; then
    echo "Welcome, Deepak!"
else
    echo "You're not Deepak."
fi
```

#### 🧠 **Use Case**:

Used when there are **two** possible outcomes — true or false — and you want to handle both.

---

### 🔹 3. `if-elif-else` Statement

#### **Syntax**:

```bash
if [ condition1 ]; then
    # commands
elif [ condition2 ]; then
    # commands
else
    # default commands
fi
```

#### ✅ **Example**:

```bash
#!/bin/bash

marks=75

if [ $marks -ge 90 ]; then
    echo "Grade: A"
elif [ $marks -ge 75 ]; then
    echo "Grade: B"
elif [ $marks -ge 50 ]; then
    echo "Grade: C"
else
    echo "Grade: F"
fi
```

#### 🧠 **Use Case**:

Used when there are **multiple conditions** and you want to execute different code blocks for each.

---

### 📌 Common Comparison Operators

| Operator | Meaning                 |
| -------- | ----------------------- |
| `-eq`    | Equal to (integers)     |
| `-ne`    | Not equal to (integers) |
| `-lt`    | Less than               |
| `-le`    | Less than or equal      |
| `-gt`    | Greater than            |
| `-ge`    | Greater than or equal   |
| `==`     | String equal            |
| `!=`     | String not equal        |
| `-z`     | String is empty         |
| `-n`     | String is not empty     |

---

### 💼 Real-World Use Case Examples

#### ✅ **Check if a file exists**

```bash
file="/etc/passwd"

if [ -f "$file" ]; then
    echo "$file exists."
else
    echo "$file does not exist."
fi
```

#### ✅ **Check user input**

```bash
echo "Enter your age:"
read age

if [ $age -ge 18 ]; then
    echo "You are eligible to vote."
else
    echo "You are not eligible to vote."
fi
```

#### ✅ **Check service status**

```bash
service="sshd"

if systemctl is-active --quiet $service; then
    echo "$service is running."
else
    echo "$service is not running."
fi
```

---

# test command and [ ], [[ ]]

In **Bash scripting**, `test`, `[ ]`, and `[[ ]]` are **used for evaluating conditional expressions** inside `if`, `elif`, or `while` statements. They differ slightly in syntax and capabilities.

---

## 🔸 1. `test` Command

### ✅ Syntax:

```bash
test condition
```

### ✅ Example:

```bash
#!/bin/bash

num=10

if test $num -gt 5; then
    echo "Number is greater than 5"
fi
```

---

## 🔸 2. `[ ]` - POSIX test command (same as `test`)

### ✅ Syntax:

```bash
if [ condition ]; then
    # commands
fi
```

### ✅ Example:

```bash
#!/bin/bash

name="Deepak"

if [ "$name" = "Deepak" ]; then
    echo "Hello, Deepak"
else
    echo "Not Deepak"
fi
```

> ✅ `[ ]` is more common than `test`. Always **quote your variables** to avoid issues with empty strings or whitespace.

---

## 🔸 3. `[[ ]]` - Bash's extended test command

### ✅ Syntax:

```bash
if [[ condition ]]; then
    # commands
fi
```

### ✅ Example:

```bash
#!/bin/bash

name="Deepak"

if [[ $name == D* ]]; then
    echo "Name starts with D"
fi
```

> ✅ `[[ ]]` is **more powerful and safer** than `[ ]`. It supports:

* Pattern matching (`==`, `!=`, glob `*`)
* Logical operators (`&&`, `||`)
* No need to quote variables in most cases

---

## 🧠 Comparison Summary

| Feature                  | `test` / `[ ]`     | `[[ ]]` (Bash-only)     |
| ------------------------ | ------------------ | ----------------------- |
| POSIX compliant          | ✅ Yes              | ❌ No                    |
| Safer with strings       | ❌ Quote needed     | ✅ Safer                 |
| Pattern matching         | ❌ No               | ✅ Yes (with `==`, `!=`) |
| Logical operators (`&&`) | ❌ Use nested if    | ✅ Yes                   |
| String with `<`, `>`     | ❌ Must quote       | ✅ No quoting needed     |
| Arithmetic expressions   | ❌ Use `-gt`, `-lt` | ❌ Same                  |

---

## 🔍 Use Cases and Examples

### 🔹 Compare Integers

```bash
a=5
b=10

if [ $a -lt $b ]; then
    echo "$a is less than $b"
fi
```

### 🔹 Compare Strings

```bash
str="hello"

if [[ $str == h* ]]; then
    echo "String starts with h"
fi
```

### 🔹 Check File Existence

```bash
file="/etc/passwd"

if [ -f "$file" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

### 🔹 Combine Conditions with `[[ ]]`

```bash
age=25
country="India"

if [[ $age -ge 18 && $country == "India" ]]; then
    echo "You can vote in India"
fi
```

### 🔹 String Empty or Not

```bash
str=""

if [ -z "$str" ]; then
    echo "String is empty"
else
    echo "String is not empty"
fi
```

---

## 🔁 With `elif` and `else`

```bash
#!/bin/bash

score=65

if [ $score -ge 90 ]; then
    echo "Grade A"
elif [ $score -ge 75 ]; then
    echo "Grade B"
elif [ $score -ge 50 ]; then
    echo "Grade C"
else
    echo "Fail"
fi
```

---

## 📦 Advanced Use Case: File Comparison

```bash
file1="file1.txt"
file2="file2.txt"

if [[ -f $file1 && -f $file2 ]]; then
    if cmp -s "$file1" "$file2"; then
        echo "Files are identical"
    else
        echo "Files are different"
    fi
else
    echo "One or both files do not exist"
fi
```

---

# Logical operators (&&, ||, !)

In **Bash scripting**, logical operators are used within `if`, `elif`, or `while` blocks to **combine multiple conditions** or **negate** them.

---

## 🔸 Logical Operators in Bash

| Operator | Description             | Use inside                           |                                |                                      |
| -------- | ----------------------- | ------------------------------------ | ------------------------------ | ------------------------------------ |
| `&&`     | Logical AND (both true) | `[[ ]]` / `(( ))` / command chaining |                                |                                      |
| \`       |                         | \`                                   | Logical OR (at least one true) | `[[ ]]` / `(( ))` / command chaining |
| `!`      | Logical NOT (negation)  | `[[ ]]` / `test` / `[ ]`             |                                |                                      |

---

### ✅ Common Conditional Contexts

1. `[[ condition1 && condition2 ]]`
2. `[[ condition1 || condition2 ]]`
3. `[[ ! condition ]]`
4. `command1 && command2` → Run `command2` **only if** `command1` succeeds
5. `command1 || command2` → Run `command2` **only if** `command1` fails

---

## 🔹 Logical AND (`&&`)

### ✅ Example 1: Check age and country

```bash
age=25
country="India"

if [[ $age -ge 18 && $country == "India" ]]; then
    echo "You are eligible to vote in India."
fi
```

### ✅ Example 2: Chaining commands

```bash
mkdir /tmp/testdir && echo "Directory created successfully"
```

> ✅ Second command only runs **if first command succeeds** (exit status 0)

---

## 🔹 Logical OR (`||`)

### ✅ Example 1: Check if user is "admin" OR "root"

```bash
user="admin"

if [[ $user == "admin" || $user == "root" ]]; then
    echo "Access granted"
else
    echo "Access denied"
fi
```

### ✅ Example 2: Chaining commands

```bash
mkdir /tmp/existing || echo "Directory already exists or cannot be created"
```

> ✅ Second command runs **only if first command fails**

---

## 🔹 Logical NOT (`!`)

### ✅ Example 1: Check if file does **not** exist

```bash
file="/tmp/data.txt"

if [[ ! -f $file ]]; then
    echo "File does not exist"
fi
```

### ✅ Example 2: Check string is not empty

```bash
str="DevOps"

if [[ ! -z "$str" ]]; then
    echo "String is not empty"
fi
```

---

## 🔹 Combining Multiple Conditions

### ✅ Example: Grade Evaluation

```bash
marks=85

if [[ $marks -ge 90 ]]; then
    echo "Grade A"
elif [[ $marks -ge 75 && $marks -lt 90 ]]; then
    echo "Grade B"
elif [[ $marks -ge 50 && $marks -lt 75 ]]; then
    echo "Grade C"
else
    echo "Fail"
fi
```

---

## 🔹 Use with Arithmetic Conditions (`(( ))`)

```bash
a=5
b=10

if (( a < b && b < 20 )); then
    echo "a is less than b and b is less than 20"
fi
```

---

## 🔹 Use with Command Exit Status

```bash
ping -c 1 google.com && echo "Internet is working" || echo "Check your connection"
```

---

## 📌 Notes:

* Prefer `[[ ]]` over `[ ]` for combining conditions.
* Use quotes around variables to avoid unexpected parsing.
* `(( ))` is only for **arithmetic** expressions.
* `!` must be **outside** the brackets: `if ! [ -f file ]`

---

## 🧠 Real-World Use Case: Script to check disk usage and send alert

```bash
#!/bin/bash

threshold=90
usage=$(df / | tail -1 | awk '{print $5}' | tr -d '%')

if [[ $usage -gt $threshold ]]; then
    echo "Disk usage is above threshold! ($usage%)"
fi
```

---


# File condition checks (-f, -d, -r, etc.)

In **Bash scripting**, file condition checks using operators like `-f`, `-d`, `-r`, `-w`, etc., allow you to test **file types** and **permissions** inside conditional blocks like `if`, `elif`, and `else`.

---

## ✅ File Test Operators in Bash

| Operator | Description                                 | True if...                            |
| -------- | ------------------------------------------- | ------------------------------------- |
| `-e`     | File exists                                 | File exists (any type)                |
| `-f`     | File is a regular file                      | File exists and is a **normal** file  |
| `-d`     | File is a directory                         | File exists and is a **directory**    |
| `-r`     | File is readable                            | File exists and can be **read**       |
| `-w`     | File is writable                            | File exists and can be **written to** |
| `-x`     | File is executable                          | File exists and is **executable**     |
| `-s`     | File exists and is not empty                | File size > 0                         |
| `!`      | Logical NOT (file does **not** exist, etc.) | Inverts the result                    |

---

## 🔸 General Syntax

```bash
if [ -f filename ]; then
    # do something
fi
```

Or using Bash's `[[`:

```bash
if [[ -f filename ]]; then
    # do something
fi
```

---

## 🔹 1. Check if File Exists

```bash
file="/etc/passwd"

if [ -e "$file" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

---

## 🔹 2. Check if Regular File

```bash
if [ -f "$file" ]; then
    echo "$file is a regular file"
fi
```

---

## 🔹 3. Check if Directory

```bash
dir="/var/log"

if [ -d "$dir" ]; then
    echo "$dir is a directory"
else
    echo "$dir is not a directory"
fi
```

---

## 🔹 4. Check File Read Permission

```bash
file="myfile.txt"

if [ -r "$file" ]; then
    echo "$file is readable"
else
    echo "$file is not readable"
fi
```

---

## 🔹 5. Check File Write Permission

```bash
if [ -w "$file" ]; then
    echo "$file is writable"
fi
```

---

## 🔹 6. Check File Execute Permission

```bash
script="install.sh"

if [ -x "$script" ]; then
    echo "Script is executable"
else
    echo "Script is not executable"
fi
```

---

## 🔹 7. Check if File is Not Empty

```bash
if [ -s "$file" ]; then
    echo "$file is not empty"
else
    echo "$file is empty"
fi
```

---

## 🔹 8. Logical NOT Example (`!`)

```bash
if [ ! -f "$file" ]; then
    echo "$file does not exist"
fi
```

---

## 🔹 9. Combining Multiple File Conditions

```bash
if [ -f "$file" ] && [ -r "$file" ]; then
    echo "$file exists and is readable"
else
    echo "$file is either missing or not readable"
fi
```

---

## 🧠 Real-World Use Case: Backup Script

```bash
backup_dir="/backup"
file="/etc/passwd"

if [ -d "$backup_dir" ] && [ -w "$backup_dir" ]; then
    cp "$file" "$backup_dir"
    echo "Backup successful"
else
    echo "Backup failed: $backup_dir is not writable"
fi
```

---

## 🧪 BONUS: File Comparison Operators

| Operator          | Description                   |
| ----------------- | ----------------------------- |
| `file1 -nt file2` | file1 is **newer than** file2 |
| `file1 -ot file2` | file1 is **older than** file2 |
| `file1 -ef file2` | Both refer to **same file**   |

```bash
if [ file1.txt -nt file2.txt ]; then
    echo "file1 is newer"
fi
```

---
# String and integer comparisons

Here’s a complete guide to **string and integer comparisons using `[[ ... ]]`** in **Bash scripting**, with `if`, `else`, `elif`, examples, and use cases. The `[[ ... ]]` syntax is **safer**, **more powerful**, and preferred for modern Bash scripts.

---

## 🔹 Why `[[ ... ]]` Over `[ ... ]`?

* Supports pattern matching (`==`, `!=`, `=~`)
* Doesn't require quoting variables (avoids word-splitting issues)
* Safer with `<`, `>`, and combined conditions (`&&`, `||`)

---

## 🧵 STRING COMPARISONS with `[[ ... ]]`

### ✅ Operators for Strings

| Operator | Meaning                            |
| -------- | ---------------------------------- |
| `==`     | Equal                              |
| `!=`     | Not equal                          |
| `<`      | Less than (lexicographic order)    |
| `>`      | Greater than (lexicographic order) |
| `-z`     | String is null (zero length)       |
| `-n`     | String is not null                 |
| `=~`     | Matches regex pattern              |

> 🔸 Note: `<` and `>` must be inside `[[ ... ]]` to avoid redirection errors.

---

### 🔸 1. Equal / Not Equal

```bash
name="deepak"

if [[ $name == "deepak" ]]; then
    echo "Welcome, Deepak!"
elif [[ $name != "deepak" ]]; then
    echo "You're not Deepak"
fi
```

---

### 🔸 2. Lexicographical Comparison

```bash
a="apple"
b="banana"

if [[ $a < $b ]]; then
    echo "$a comes before $b"
else
    echo "$a comes after or is equal to $b"
fi
```

---

### 🔸 3. Check if String is Empty / Not Empty

```bash
str=""

if [[ -z $str ]]; then
    echo "String is empty"
fi

str="DevOps"
if [[ -n $str ]]; then
    echo "String is not empty"
fi
```

---

### 🔸 4. Pattern Matching with `=~` (regex)

```bash
email="test@example.com"

if [[ $email =~ ^[a-zA-Z0-9._%+-]+@example\.com$ ]]; then
    echo "Valid corporate email"
else
    echo "Invalid email domain"
fi
```

---

## 🔢 INTEGER COMPARISONS with `[[ ... ]]` + `(( ... ))`

You can use:

* `[[ $a -eq $b ]]` → older integer operators inside `[[ ]]`
* or prefer `(( ... ))` for **arithmetic** evaluation

---

### ✅ Integer Operators (inside `[[ ... ]]`)

| Operator | Meaning               |
| -------- | --------------------- |
| `-eq`    | Equal                 |
| `-ne`    | Not equal             |
| `-lt`    | Less than             |
| `-le`    | Less than or equal    |
| `-gt`    | Greater than          |
| `-ge`    | Greater than or equal |

---

### 🔸 1. Using `[[ ... ]]` with Integer Operators

```bash
age=25

if [[ $age -ge 18 && $age -le 60 ]]; then
    echo "Eligible age group"
fi
```

---

### 🔸 2. Using `(( ... ))` (more intuitive for math)

```bash
a=10
b=5

if (( a > b )); then
    echo "$a is greater than $b"
fi
```

---

### 🔸 3. If-elif-else Example for Grades

```bash
score=67

if [[ $score -ge 90 ]]; then
    echo "Grade A"
elif [[ $score -ge 75 ]]; then
    echo "Grade B"
elif [[ $score -ge 50 ]]; then
    echo "Grade C"
else
    echo "Fail"
fi
```

---

### 🔸 4. Combined Conditions (Logical AND / OR)

```bash
user="admin"
logged_in=true

if [[ $user == "admin" && $logged_in == true ]]; then
    echo "Admin access granted"
fi
```

```bash
os="linux"
shell="zsh"

if [[ $os == "linux" || $shell == "bash" ]]; then
    echo "Supported environment"
fi
```

---

## 📦 Real-World Use Cases

### ✅ Validate User Input

```bash
read -p "Enter a number: " num

if [[ $num =~ ^[0-9]+$ ]]; then
    echo "Valid number"
else
    echo "Invalid input"
fi
```

---

### ✅ Check Environment and Version

```bash
version="3.9"
os="ubuntu"

if [[ $os == "ubuntu" && $version == "3.9" ]]; then
    echo "Ready for deployment"
fi
```

---

### ✅ Regex: Validate Phone Number

```bash
phone="9876543210"

if [[ $phone =~ ^[0-9]{10}$ ]]; then
    echo "Valid phone number"
else
    echo "Invalid phone number"
fi
```

---

## ✅ Summary

| Type    | Preferred Syntax             | Example                                  |         |                               |
| ------- | ---------------------------- | ---------------------------------------- | ------- | ----------------------------- |
| String  | `[[ $a == $b ]]`             | `[[ $name == "Deepak" ]]`                |         |                               |
| Integer | `[[ $a -gt $b ]]` or `(( ))` | `(( age >= 18 ))` or `[[ $age -ge 18 ]]` |         |                               |
| Pattern | `[[ $var =~ regex ]]`        | `[[ $email =~ @example\.com$ ]]`         |         |                               |
| Logic   | `&&`, \`                     |                                          | `, `!\` | `[[ $a -gt 5 && $b -lt 10 ]]` |

---







