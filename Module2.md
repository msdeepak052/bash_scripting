## 🧾 1. What is Shell Scripting?

**Shell scripting** is writing a set of commands in a file (script) that the shell can execute. It's widely used in Linux for automation, system administration, DevOps, and development tasks.

> **Shell**: A command-line interpreter (like `bash`, `sh`, `zsh`).
> **Shell Script**: A text file with a list of shell commands to be executed.

---

## 🏁 2. Basic Shell Script Structure

```bash
#!/bin/bash        # 👈 Shebang - tells the system to use Bash shell
# This is a comment

echo "Hello, World!"    # 👈 Print statement
```

> Save this as `script.sh` and run with:
> `chmod +x script.sh`
> `./script.sh`

---

## 📢 3. Printing in Shell: `echo` and `printf`

---

### ✅ `echo` Command

Used to **display messages** on the terminal.

```bash
echo "Hello Deepak!"
```

---

### ⚙️ Common `echo` Options/Parameters

| Option | Description                                | Example                  |
| ------ | ------------------------------------------ | ------------------------ |
| `-n`   | Do not add a newline                       | `echo -n "Hello"`        |
| `-e`   | Enable interpretation of backslash escapes | `echo -e "Line1\nLine2"` |
| `-E`   | Disable interpretation (default)           | `echo -E "Hello\nWorld"` |

---

### 🔠 Common Escape Characters (when `-e` is used)

| Escape | Description  | Example                             |
| ------ | ------------ | ----------------------------------- |
| `\n`   | New line     | `echo -e "Line1\nLine2"`            |
| `\t`   | Tab          | `echo -e "Name:\tDeepak"`           |
| `\\`   | Backslash    | `echo -e "This is a backslash: \\"` |
| `\"`   | Double quote | `echo -e "He said: \"Hello\""`      |
| `\a`   | Alert sound  | `echo -e "\a"`                      |

---

#### 🧪 `echo` Examples

```bash
echo "Simple message"

echo -n "No newline at end"

echo -e "Name:\tDeepak\nLocation:\tIndia"

echo -E "No special char interpretation: \n\t"
```

---

## 📌 4. `printf` - More Control over Output

`printf` works like C’s `printf()` function and gives more formatting control than `echo`.

### 🔢 Syntax

```bash
printf "FORMAT_STRING" [ARGUMENTS...]
```

---

### 🔡 Format Specifiers

| Specifier | Meaning | Example    |
| --------- | ------- | ---------- |
| `%s`      | String  | `"Deepak"` |
| `%d`      | Integer | `25`       |
| `%f`      | Float   | `3.14`     |
| `%x`      | Hex     | `255`      |
| `%c`      | Char    | `A`        |

---

### 🧪 `printf` Examples

```bash
printf "Hello %s!\n" "Deepak"
printf "Number: %d\n" 100
printf "Float: %.2f\n" 3.14159
printf "%-10s %10s\n" "Name" "Score"
```

> `%-10s` means left-aligned 10 chars, `%10s` means right-aligned 10 chars.

---

## 📝 5. Sample Full Shell Script

```bash
#!/bin/bash

# Define variables
name="Deepak"
age=25

# Print with echo
echo "Welcome to shell scripting!"
echo -e "Name:\t$name\nAge:\t$age"

# Print with printf
printf "Hello %s, your age is %d\n" "$name" "$age"
```

---

## 📦 6. Advanced echo with Variables and Commands

```bash
name="Deepak"
echo "Hello, $name!"

# Command substitution
echo "Current date is: $(date)"

# Using variables inside echo
file="data.txt"
echo "Processing file: $file"
```

---

## 📁 7. Input & Output Redirection

```bash
echo "Hello" > file.txt     # Write to file
echo "Again" >> file.txt    # Append to file

cat file.txt                # Display file content
```

---

## 🧯 8. Error and Debug

```bash
echo "This goes to stdout"
echo "This is an error" >&2      # Print to stderr

# Debugging output
set -x       # Enable debug mode
echo "Debug me"
set +x       # Disable debug mode
```

---

## 🛠️ 9. Interactive Shell Script Example

```bash
#!/bin/bash

read -p "Enter your name: " username
echo "Hi $username, welcome to DevOps world!"
```

---

## ✅ Summary

| Command    | Use Case                                |
| ---------- | --------------------------------------- |
| `echo`     | Basic printing (less formatting)        |
| `printf`   | Advanced printing (alignment, decimals) |
| `-e`       | Enable escapes (`\n`, `\t`) in `echo`   |
| `read`     | Input from user                         |
| `>` / `>>` | Redirect output to file                 |
| `set -x`   | Debug script execution                  |

---
## Variable in Shell

Let's dive into **Variables in Shell Scripting**, including **Local and Environment Variables**, with clear examples and detailed explanations of **all relevant parameters and use cases**.

---

## 🧾 1. What is a Variable in Shell?

A **variable** is a name that refers to a value. Variables in shell scripting store data like strings, numbers, filenames, etc., and make scripts dynamic.

---

## 🧠 2. Types of Shell Variables

| Type                     | Scope                               | Persistency                        |
| ------------------------ | ----------------------------------- | ---------------------------------- |
| **Local Variable**       | Only inside current shell or script | Temporary (lost after shell exits) |
| **Environment Variable** | Available to child processes        | Can be made persistent in profiles |

---

## 🧪 3. Local Variables

### ✅ Syntax

```bash
variable_name=value     # No spaces around '='
```

### 🧪 Examples

```bash
name="Deepak"
age=30

echo "Name: $name"
echo "Age: $age"
```

### ❗ Rules for Variable Names

* Must start with a letter or underscore (`_`)
* Can contain letters, numbers, or underscores
* No spaces around `=`
* Case-sensitive: `MyVar` ≠ `myvar`

---

## 📦 4. Using Variables

```bash
greeting="Hello"
name="Deepak"
echo "$greeting, $name!"    # Output: Hello, Deepak!
```

---

## 💡 5. Quoting Variables

```bash
name="Deepak Yadav"
echo $name         # Word splitting happens
echo "$name"       # Proper handling with quotes
```

> ✅ Always quote variables to avoid word splitting and globbing issues.

---

## 🧪 6. Environment Variables

These are special variables available system-wide or to child processes.

### ✅ Declaring Environment Variables

```bash
export MYVAR="This is environment variable"
```

### 🧪 Example

```bash
export PROJECT="DevOpsApp"
bash -c 'echo "Project is $PROJECT"'   # Accessible in child shell
```

---

## 🛠️ 7. Viewing All Environment Variables

```bash
printenv              # Only environment variables
env                   # Similar to printenv
set                   # Shows all shell + env variables
```

---

## 🚫 8. Unsetting Variables

```bash
unset name
echo $name     # Will print nothing
```

---

## 🧪 9. Default & Conditional Variable Expansion

| Syntax            | Description                             | Example                      |
| ----------------- | --------------------------------------- | ---------------------------- |
| `${var:-default}` | Use default if var is unset or empty    | `echo ${name:-Guest}`        |
| `${var:=default}` | Assign default if var is unset or empty | `echo ${name:=Guest}`        |
| `${var:+alt}`     | Use alt if var is set                   | `echo ${name:+Hi}`           |
| `${var:?error}`   | Error if var is unset                   | `echo ${name:?Name not set}` |

---

### 🧪 Examples

```bash
echo ${username:-"Anonymous"}   # If $username not set, use Anonymous

username=""
echo ${username:-"Anonymous"}   # Still uses Anonymous

echo ${username:="SetDefault"}  # Sets username to SetDefault if not set

unset city
echo ${city:?"City is not set!"}  # Prints error and exits if city unset
```

---

## 📁 10. Making Environment Variables Permanent

### 🛠️ Add to config files like `.bashrc`, `.bash_profile`, `.profile`

```bash
echo 'export PATH=$PATH:/opt/myapp/bin' >> ~/.bashrc
source ~/.bashrc
```

---

## 🧪 11. Special Shell Variables (Built-in)

| Variable | Description                       |
| -------- | --------------------------------- |
| `$0`     | Script name                       |
| `$1..$n` | Positional args                   |
| `$#`     | Number of args                    |
| `$@`     | All args (individually quoted)    |
| `$*`     | All args (single string)          |
| `$$`     | Current PID                       |
| `$?`     | Exit status of last command       |
| `$_`     | Last argument of previous command |

---

## 💡 12. Using `declare` (Advanced)

```bash
declare myvar="Hello"         # Normal variable
declare -i num=100            # Integer only
declare -r const="readonly"   # Readonly
declare -x envvar="Exported"  # Environment variable
```

---

### `declare` Flags Summary

| Flag | Description                        |
| ---- | ---------------------------------- |
| `-i` | Treat variable as integer          |
| `-r` | Read-only (can't modify later)     |
| `-x` | Export (make environment variable) |
| `-a` | Declare array                      |
| `-f` | Show functions                     |
| `-p` | Display declared vars              |

---

## 🧪 Practical Example: Script with Local & Environment Variables

```bash
#!/bin/bash

# Local variables
user="Deepak"
echo "User: $user"

# Environment variable
export APP_ENV="dev"
bash -c 'echo "Environment: $APP_ENV"'

# Conditional default
echo "Region: ${REGION:-us-east-1}"

# Integer example
declare -i count=5
count=$count+1
echo "Count: $count"
```

---

## ✅ Summary Table

| Feature     | Local                 | Environment                         |
| ----------- | --------------------- | ----------------------------------- |
| Scope       | Current shell         | Available to child processes        |
| Declared by | `var=value`           | `export var=value`                  |
| Visibility  | Lost when shell exits | Used across sessions (if persisted) |
| Tools       | `set`                 | `printenv`, `env`                   |

---

# **Data Types in Shell Scripting** 
---

## 🧾 1. Overview of Data Types in Shell

| Data Type                       | Description                           |
| ------------------------------- | ------------------------------------- |
| **String**                      | Sequence of characters (default type) |
| **Integer**                     | Numeric value (used for arithmetic)   |
| **Array**                       | Ordered list of elements              |
| **Associative Array** (Bash 4+) | Key-value pairs                       |

---

## 🔠 2. **Strings** (Default type)

### ✅ Declaration

```bash
name="Deepak"
msg='Hello World'
multi_line="Line1
Line2"
```

> ⚠️ **No space around `=`** when assigning.

---

### 📢 Access and Print

```bash
echo "$name"
echo "$msg"
```

---

### 🔧 String Operations

| Operation | Syntax                           | Example                |
| --------- | -------------------------------- | ---------------------- |
| Length    | `${#var}`                        | `${#name}` → `6`       |
| Substring | `${var:pos}` or `${var:pos:len}` | `${name:1:3}` → `eep`  |
| Replace   | `${var/pattern/repl}`            | `${msg/Hello/Hi}`      |
| Uppercase | `${var^^}`                       | `${name^^}` → `DEEPAK` |
| Lowercase | `${var,,}`                       | `${name,,}` → `deepak` |

---

### 🧪 String Example

```bash
name="Deepak"
echo "Length: ${#name}"
echo "First 3: ${name:0:3}"
echo "Replace: ${name/Deep/Dev}"
echo "Uppercase: ${name^^}"
```

---

## 🔢 3. **Integers**

### ✅ Declaration

```bash
num1=10
num2=20
```

> Bash treats everything as a string unless explicitly declared.

---

### ⚙️ Enable Integer Behavior

```bash
declare -i count=100
count+=1
echo "Count: $count"
```

---

### ➕ Arithmetic Operations

Use `$(( ))` for integer arithmetic:

```bash
a=5
b=3
sum=$((a + b))     # Add
diff=$((a - b))    # Subtract
prod=$((a * b))    # Multiply
div=$((a / b))     # Divide
mod=$((a % b))     # Modulo

echo "Sum: $sum"
```

---

### ➕ Example with `let` and `expr`

```bash
let result=5+5
echo "Result: $result"

result=$(expr 5 + 5)
echo "Result: $result"
```

> `expr` needs spaces and backticks/command substitution.

---

## 🧮 Comparison (Integer)

```bash
a=5
b=10

if (( a < b )); then
  echo "$a is less than $b"
fi
```

---

## 📚 4. **Arrays**

> Arrays hold multiple values and are **0-indexed**.

### ✅ Declare & Assign

```bash
# Declare array
arr=("apple" "banana" "cherry")

# Assign using index
arr[3]="date"
```

---

### 📢 Access Elements

```bash
echo "${arr[0]}"         # apple
echo "${arr[1]}"         # banana
```

---

### 🔁 Loop Through Array

```bash
for fruit in "${arr[@]}"; do
  echo "Fruit: $fruit"
done
```

---

### 📏 Array Length

```bash
echo "Length: ${#arr[@]}"
```

---

### 🔧 Array Slicing & Index

```bash
echo "All: ${arr[@]}"
echo "Slice: ${arr[@]:1:2}"     # banana cherry
```

---

### 🧪 Array Example

```bash
colors=("red" "green" "blue")
echo "First: ${colors[0]}"
colors[1]="yellow"
echo "Updated: ${colors[@]}"
```

---

## 🔑 5. **Associative Arrays** (Bash 4+)

### ✅ Declare & Use

```bash
declare -A user
user[name]="Deepak"
user[role]="DevOps"
```

---

### 📢 Access Associative Array

```bash
echo "${user[name]}"
echo "${user[role]}"
```

---

### 🔁 Looping Through Keys

```bash
for key in "${!user[@]}"; do
  echo "$key => ${user[$key]}"
done
```

---

## 🧮 6. Comparison Summary

### String Comparisons

```bash
str1="apple"
str2="banana"

if [[ "$str1" == "$str2" ]]; then
  echo "Equal"
else
  echo "Not equal"
fi
```

| Operator  | Meaning            |
| --------- | ------------------ |
| `==`      | Equal              |
| `!=`      | Not equal          |
| `<` / `>` | Lexical comparison |

---

### Integer Comparison

| Expression | Meaning               |
| ---------- | --------------------- |
| `-eq`      | equal                 |
| `-ne`      | not equal             |
| `-lt`      | less than             |
| `-le`      | less than or equal    |
| `-gt`      | greater than          |
| `-ge`      | greater than or equal |

---

### Example

```bash
a=10
b=20

if [ $a -lt $b ]; then
  echo "$a is less than $b"
fi
```

---

## 🛠️ 7. Declaring with `declare` and `typeset`

| Syntax                        | Description       |
| ----------------------------- | ----------------- |
| `declare -i var=5`            | Integer           |
| `declare -a arr=(1 2 3)`      | Indexed array     |
| `declare -A map=()`           | Associative array |
| `declare -r CONST="readonly"` | Read-only         |
| `declare -x VAR=value`        | Export as env var |

---

## ✅ Final Script Example (All Types)

```bash
#!/bin/bash

# String
name="Deepak"
echo "Name: ${name^^}"

# Integer
declare -i age=25
age+=5
echo "Age: $age"

# Array
fruits=("apple" "banana" "cherry")
echo "Fruits: ${fruits[@]}"

# Associative Array
declare -A user
user[name]="Deepak"
user[role]="DevOps"
echo "User Role: ${user[role]}"
```

---

## 📌 Summary

| Type         | Syntax                   | Notes                          |
| ------------ | ------------------------ | ------------------------------ |
| String       | `var="text"`             | Default type                   |
| Integer      | `declare -i` or `$(( ))` | Arithmetic only works this way |
| Array        | `arr=(val1 val2)`        | Index-based                    |
| Assoc. Array | `declare -A`             | Key-value (Bash 4+)            |

---

Understanding how **quotes** work in **Bash** is essential because quoting affects **how variables and commands are interpreted**. Here's a detailed explanation of **single quotes `'`, double quotes `"`, and backticks `` ` `` (along with `$( )`)** with **examples, parameters, and best practices**.

---

## 🧾 1. Why Quotes Matter in Shell

In shell scripting, **quoting determines how the shell parses your command**—whether it treats variables and commands literally or evaluates them.

---

## 🔴 2. **Single Quotes (`'`)** – Literal Quotes

### ✅ Behavior:

* Treat everything **literally**
* **No variable expansion**
* **No command substitution**
* **No escape character interpretation**

---

### 🔧 Syntax:

```bash
'text'
```

---

### 🧪 Example:

```bash
name="Deepak"

echo 'Hello $name'         # Output: Hello $name
```

> It **prints `$name`** as a string, not its value.

---

### ⚠️ Notes:

* You **cannot escape characters** inside single quotes.
* To include a `'` inside `'...'`, you need to close and reopen quotes:

```bash
echo 'It'\''s working'     # Output: It's working
```

---

## 🟡 3. **Double Quotes (`"`)** – Expandable Quotes

### ✅ Behavior:

* Allows **variable expansion**
* Allows **command substitution**
* Supports **escape sequences** (`\n`, `\t`, etc.)

---

### 🔧 Syntax:

```bash
"text with $variables and $(commands)"
```

---

### 🧪 Examples:

```bash
name="Deepak"
echo "Hello $name"               # Output: Hello Deepak

echo "Today is $(date)"          # Output: Today is Sun Jul 14 ...

echo "Path: \$PATH"              # Escapes $

echo "Multi-line\nNext line"     # Prints as-is unless with -e
```

> You can escape characters like `$`, `"`, `` ` ``, `\` using `\`.

---

## 🟢 4. **Backticks (`` `command` ``)** – Command Substitution (Old Style)

### ✅ Behavior:

* Executes the command inside and replaces it with the result (like `$(...)`)
* Deprecated in favor of `$(...)` because of nesting issues

---

### 🔧 Syntax:

```bash
`command`
```

---

### 🧪 Example:

```bash
echo "Current directory is: `pwd`"
```

> Output: Current directory is: `/home/deepak`

---

### ⚠️ Backtick Limitation:

```bash
# Difficult to nest:
echo "`echo \`date\``"       # Confusing and error-prone
```

---

## ✅ 5. Preferred: **Command Substitution with `$(...)`**

Modern and readable way to run a command and use its output.

---

### 🧪 Examples:

```bash
today=$(date +%Y-%m-%d)
echo "Today is $today"
```

> 👍 Easier to read and supports nesting:

```bash
echo "Nested: $(echo $(date))"
```

---

## 🔁 6. Summary Table

| Quote Type      | Allows Variables | Allows Commands | Escape Interpretation    | Usage                                |
| --------------- | ---------------- | --------------- | ------------------------ | ------------------------------------ |
| `'` (Single)    | ❌ No             | ❌ No            | ❌ No                     | Use for literal strings              |
| `"` (Double)    | ✅ Yes            | ✅ Yes           | ✅ Yes                    | Use for interpolated strings         |
| `` `command` `` | N/A              | ✅ Yes           | ❌ No                     | Deprecated (use `$(...)`)            |
| `$(command)`    | N/A              | ✅ Yes           | ✅ Yes (outside `"` only) | ✅ Preferred for command substitution |

---

## 🛠️ 7. Practical Script Example Using All

```bash
#!/bin/bash

name="Deepak"
greeting='Welcome'

# Single quotes (no expansion)
echo 'Hello $name, today is `date`'

# Double quotes (expansion)
echo "Hello $name, today is $(date)"

# Command substitution with backticks (old)
echo "Uptime: `uptime`"

# Modern command substitution
today=$(date +%A)
echo "Happy $today, $name!"
```

---

## 🧪 8. Real-world Use Case: Generating a File with Dynamic Content

```bash
#!/bin/bash

username="deepak"
today=$(date)

cat <<EOF
Hello $username!
Today is: $today
Your current directory: $(pwd)
EOF
```

> Uses **double-quoted heredoc** (`<<EOF`) for variable and command expansion.

---

## ⚠️ 9. Common Mistakes

| Mistake                            | Fix                                               |
| ---------------------------------- | ------------------------------------------------- |
| `echo '$HOME'`                     | Won’t expand. Use `echo "$HOME"`                  |
| Mixing `'` and `"`                 | Don’t nest `'` inside `'...'`. Use concatenation. |
| Using backticks in nested commands | Use `$(...)` instead                              |

---

## ✅ Conclusion

* Use `'` when you want **literal** text
* Use `"` when you want **variable or command expansion**
* Use `$(...)` instead of `` `...` `` for **command substitution**
* Always quote variables (`"$var"`) to **avoid word splitting**

---

# **Comments and Documentation in Shell Scripts**

---

## 🧾 1. What are Comments in Shell Scripting?

**Comments** are lines ignored by the shell interpreter but **read by humans** to explain the code.
They are helpful for:

* Documenting logic
* Explaining complex commands
* Temporarily disabling code (debugging)
* Adding metadata (author, version, usage)

---

## 🔰 2. Single-Line Comments

### ✅ Syntax:

```bash
# This is a comment
```

### 🧪 Example:

```bash
#!/bin/bash

# This script prints the current date
echo "Today's date is: $(date)"
```

> Everything after `#` on a line is treated as a comment, unless it's inside quotes.

---

## 🔁 3. Inline Comments

```bash
echo "Hello, Deepak!"   # Greet the user
```

> ⚠️ Inline comments must have a space before `#` to be valid.

---

## 🧯 4. Commenting Out Code (Temporary Disable)

```bash
# echo "This line is disabled"
```

---

## 🧾 5. Multi-Line Comments (Workarounds)

Shell doesn't support real multi-line comments natively. Use one of these:

### ✅ Method 1: Multiple `#` Lines

```bash
# This is a multi-line comment
# It explains the block below
# that performs a backup operation
```

### ✅ Method 2: `: <<'COMMENT'` (Here Document Trick)

```bash
: <<'END_COMMENT'
This entire block is commented.
It will not be executed by the shell.
You can add documentation here too.
END_COMMENT
```

---

## 📋 6. Script Header Documentation (Shebang + Metadata)

Add this at the top of your script for documentation purposes:

```bash
#!/bin/bash
#
# Script Name: backup.sh
# Author: Deepak Yadav
# Created: 13-Jul-2025
# Purpose: Performs backup of /home directory
# Usage: ./backup.sh
# Notes: Ensure you have write permissions
#
```

---

## 🧪 Example Script with Comments & Documentation

```bash
#!/bin/bash
#
# Script: welcome.sh
# Author: Deepak
# Date: 13-Jul-2025
# Description: Greets the user and shows system info

# Ask for the user's name
read -p "Enter your name: " username

# Greet the user
echo "Hello, $username! Welcome to DevOps!"

# Show current date and uptime
echo "Date: $(date)"          # Current system date
echo "Uptime: $(uptime)"      # System uptime
```

---

## 💡 7. Best Practices for Commenting

✅ Do:

* Use comments to **explain why**, not just what
* **Document assumptions** and known issues
* Include script **metadata** at the top
* Keep comments **up-to-date**

🚫 Don’t:

* Over-comment obvious code (`# add 1 to i`)
* Leave stale or misleading comments

---

## 📌 Summary

| Feature     | Syntax               | Purpose                    |
| ----------- | -------------------- | -------------------------- |
| Single-line | `#`                  | Short explanation          |
| Inline      | `command  # comment` | Notes beside command       |
| Multi-line  | `: <<'COMMENT'`      | Large block (not executed) |
| Script doc  | `#` header block     | Author, date, usage, etc.  |

---

# **Read input from the user in shell scripting**
---

## 🧾 1. What is `read`?

The `read` command **reads a line of input from the user (stdin)** and stores it in a variable.

---

## ✅ 2. Basic Syntax

```bash
read variable_name
```

### 🧪 Example

```bash
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

---

## ⚙️ 3. `read` with `-p` (Prompt)

Display a prompt without using a separate `echo`:

```bash
read -p "Enter your city: " city
echo "You live in $city"
```

---

## 🔒 4. `read` with `-s` (Silent/Hidden Input)

Used for **password input**:

```bash
read -sp "Enter your password: " password
echo -e "\nPassword received (but hidden)"
```

> `-s` hides the input as the user types.

---

## 🕒 5. `read` with `-t` (Timeout)

Specify a timeout (in seconds):

```bash
read -t 5 -p "Enter your username (5 sec timeout): " username
echo "You entered: $username"
```

> If no input is given within 5 seconds, `read` exits with failure.

---

## 🧠 6. `read` with `-n` (Limit Characters)

Read only a specific number of characters (without Enter):

```bash
read -n 1 -p "Press any key to continue..." key
echo -e "\nYou pressed: $key"
```

---

## 🧪 7. Reading Multiple Variables

```bash
read -p "Enter your first and last name: " fname lname
echo "First: $fname, Last: $lname"
```

> Input is split by spaces. Extra input goes to the last variable.

---

## 🔄 8. Reading Input in Loops

```bash
while read line; do
  echo "Line: $line"
done < file.txt
```

> Reads each line of a file.

---

## 🛠️ 9. Full Example with All Options

```bash
#!/bin/bash

read -p "Username: " username
read -sp "Password: " password
echo -e "\nWelcome $username!"
```

---

## 📌 Summary of `read` Options

| Option | Description                                  |
| ------ | -------------------------------------------- |
| `-p`   | Prompt before reading input                  |
| `-s`   | Silent (hidden input)                        |
| `-t`   | Timeout in seconds                           |
| `-n`   | Read N characters only                       |
| `-a`   | Store input into an array                    |
| `-r`   | Raw mode (don’t treat backslashes specially) |

---

## 💡 Best Practices

* Always quote variables: `"$name"`
* Use `-s` for passwords
* Use timeouts (`-t`) for automated scripts
* Use `-p` for clean prompts

---

Great topic Deepak! Let's clearly understand the differences and usage of **`exit`**, **`return`**, and **exit status (`$?`)** in shell scripting — with syntax, examples, and best practices.

---

## 🧾 1. What is **Exit Status**?

In shell scripting, **every command returns an exit status** (an integer) to indicate **success** or **failure**:

| Code    | Meaning                                       |
| ------- | --------------------------------------------- |
| `0`     | Success                                       |
| `1–255` | Failure (non-zero means something went wrong) |

# **Exit status of the last executed command**

```bash
echo $?
```

---

### 🧪 Example

```bash
#!/bin/bash

ls /tmp
echo "Exit status of ls: $?"   # Likely 0

ls /notfound
echo "Exit status of ls: $?"   # Likely non-zero (e.g., 2)
```

---

## 🚪 2. `exit` – Exit a script or shell

### ✅ Syntax:

```bash
exit [status_code]
```

* Ends the current script immediately
* Optionally sets a return code (0–255)

---

### 🧪 Example: Using `exit` in Script

```bash
#!/bin/bash

echo "Start"
exit 1
echo "This won't print"
```

> The script **exits at `exit 1`**, skipping the rest.

---

## 🔁 3. `return` – Exit a function with a status

### ✅ Syntax:

```bash
return [status_code]
```

* Used **inside functions only**
* Returns control to the caller

---

### 🧪 Example: `return` in Function

```bash
#!/bin/bash

check_age() {
  if [ $1 -lt 18 ]; then
    echo "Underage"
    return 1
  else
    echo "Adult"
    return 0
  fi
}

check_age 15
echo "Status: $?"
```

---

## ❗ 4. Differences: `exit` vs `return`

| Feature   | `exit`             | `return`            |
| --------- | ------------------ | ------------------- |
| Used in   | Script or function | Function only       |
| Purpose   | Exit script/shell  | Exit function       |
| Affects   | Entire script      | Only function scope |
| Sets `$?` | ✅ Yes              | ✅ Yes               |

---

## 💡 5. Using Exit Codes in `if` Statements

```bash
if some_command; then
  echo "Success"
else
  echo "Failed"
fi
```

> This is a cleaner way than checking `$?` manually.

---

## 🛠️ 6. Custom Exit Status Codes

Define your own codes for clarity:

```bash
#!/bin/bash

if ! ping -c 1 google.com &>/dev/null; then
  echo "Network unreachable"
  exit 101
fi
```

---

## 📋 7. Standard Exit Code Examples (for reference)

| Code  | Description                         |
| ----- | ----------------------------------- |
| `0`   | Success                             |
| `1`   | General error                       |
| `2`   | Misuse of shell command             |
| `126` | Command invoked cannot execute      |
| `127` | Command not found                   |
| `130` | Script terminated by Ctrl+C         |
| `255` | Exit status out of range (overflow) |

---

## 🔁 8. Full Example: Exit vs Return

```bash
#!/bin/bash

say_hello() {
  echo "Inside function"
  return 0
}

say_hello
echo "Returned with: $?"

exit 0
```

---

## ✅ Best Practices

* Use `exit 0` for success, `exit 1` (or custom codes) for failure
* Use `return` only inside functions
* Always handle critical commands with exit status
* Chain commands logically:

```bash
command1 && command2   # Run command2 only if command1 succeeded
command1 || command2   # Run command2 only if command1 failed
```

---

## 🔍 Final Summary

| Command  | Use Case                         | Scope         | Sets `$?` |
| -------- | -------------------------------- | ------------- | --------- |
| `exit`   | Terminate script with status     | Script-wide   | ✅         |
| `return` | End a function and return status | Function only | ✅         |
| `$?`     | Get last command’s exit status   | Any shell     | ✅         |

---
