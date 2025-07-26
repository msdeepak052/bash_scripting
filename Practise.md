# Bash Scripting Practise Questions

Here's a **module-wise collection of 15 shell scripting coding questions** per module (no theory), followed by **answers at the end**. I’ve also added a few **real-world/practical scripting questions** in each section.

---

## ✅ **Module 1: Introduction to Shell and Bash – 15 Coding Questions**

1. Write a script to print "Hello DevOps" using `#!/bin/bash`.

<img width="1160" height="731" alt="image" src="https://github.com/user-attachments/assets/7c280954-72d0-47df-9657-8cb59c66ca69" />

2. Create a script that prints your current shell and username.

<img width="1143" height="789" alt="image" src="https://github.com/user-attachments/assets/5a8bc937-88ea-4c2a-948f-93a1b2facede" />

3. Print the list of all shells available in the system.

```bash
#!/bin/bash

# Get the list of shells from /etc/shells

while IFS= read -r line; do
    echo "$line"
done < /etc/shells
```
```bash
/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/sh
/bin/dash
/usr/bin/dash
/usr/bin/tmux
/usr/bin/screen
```

4. Create a script that prints the current directory using a command shortcut.

<img width="1057" height="564" alt="image" src="https://github.com/user-attachments/assets/5af485b0-12e4-4cc8-8d9a-2858e25ed06e" />

5. Create a script with incorrect shebang and observe behavior.

<img width="980" height="553" alt="image" src="https://github.com/user-attachments/assets/9b0f4772-6a87-49d5-808e-cdf5c03a3e6e" />

6. Use history expansion to repeat the last command in a script.
7. Display script name and number of arguments passed.

```bash
#!/bin/bash

echo "Script Name : $0"
echo "Number of arguments : $#"
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Script Name : ./test.sh
Number of arguments : 0
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh Deepak
Script Name : ./test.sh
Number of arguments : 1
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ 
```

8. Write a script to display current shell type using `$SHELL`.

``` Refer Question 2 ```

9. Show all environment variables from a script.

```bash
#!/bin/bash

echo "Environment Variables: $(env)" | sort
```

10. Use alias in a script to replace `ls -l` with `ll`.

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ alias ll='ls -lhrt'
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ll
total 4.0K
-rwxrwxrwx 1 deepak deepak 248 Jul 11 18:10 data.txt
-rwxrwxrwx 1 deepak deepak 385 Jul 11 18:44 sales.csv   
-rw-r--r-- 1 deepak deepak 187 Jul 11 19:36 5fields.txt 
-rwxrwxrwx 1 deepak deepak  96 Jul 11 19:42 expenses.csv
-rwxrwxrwx 1 deepak deepak  99 Jul 13 23:30 students.csv
-rwxrwxrwx 1 deepak deepak 137 Jul 14 00:13 unique.csv
-rwxrwxrwx 1 deepak deepak 230 Jul 14 00:19 employees.csv
-rwxrwxrwx 1 deepak deepak 144 Jul 14 00:22 salary.csv
-rwxrwxrwx 1 deepak deepak 383 Jul 14 00:34 ip.txt
-rwxrwxrwx 1 deepak deepak 107 Jul 14 00:37 awk1.sh
-rwxrwxrwx 1 deepak deepak 128 Jul 15 23:20 test.py
-rwxrwxrwx 1 deepak deepak  56 Jul 22 10:31 test.sh
```

11. Create a script and run it with `bash script.sh` and `./script.sh`. Observe differences.

 Let's walk through this step-by-step to understand the differences between:

* Running a script via: `bash script.sh`
* Running a script via: `./script.sh`

---

### 📝 Step 1: Create a test script

Create a script named `script.sh` with the following content:

```bash
#!/bin/bash

echo "Current shell: $SHELL"
echo "Script executed with: $0"
```

Save the file in your directory.

---

### 🧪 Step 2: Run the script both ways

#### ✅ Method 1: `bash script.sh`

```bash
bash script.sh
```

#### ✅ Method 2: `./script.sh`

First, make it executable:

```bash
chmod +x script.sh
./script.sh
```

---

### 🔍 Expected Output Comparison

#### Output of `bash script.sh`:

```
Current shell: /bin/bash
Script executed with: script.sh
```

#### Output of `./script.sh`:

```
Current shell: /bin/bash
Script executed with: ./script.sh
```

---

### ⚙️ What's the Difference?

| Aspect                     | `bash script.sh`                              | `./script.sh`                                      |
| -------------------------- | --------------------------------------------- | -------------------------------------------------- |
| **Interpreter**            | Uses explicitly `bash`, regardless of shebang | Uses shebang (`#!/bin/bash`) to decide interpreter |
| **\$0 value**              | `script.sh`                                   | `./script.sh`                                      |
| **Execution**              | Script run **as a parameter** to bash         | Script run **as an executable file**               |
| **Exec permission needed** | ❌ Not needed                                  | ✅ Required (`chmod +x`)                            |
| **Overrides shebang?**     | ✅ Yes                                         | ❌ No, it uses it                                   |

---

### ✅ Summary

* Use `bash script.sh` if you're debugging or testing with a specific shell.
* Use `./script.sh` to execute the script like a standalone program (respects shebang).
* Both are valid, but behave slightly differently in how they pass arguments and set `$0`.



12. Store the output of `pwd` in a variable and print it.

```bash
#!/bin/bash

current_working_directory=$(pwd)
echo "Current Working Directory: $current_working_directory"
````

13. Write a script to check whether the current shell is interactive or not.

```bash
#!/bin/bash

# Check if shell is interactive
case $- in
  *i*) 
    echo "The shell is interactive."
    ;;
  *)  
    echo "The shell is NOT interactive."
    ;;
esac
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
The shell is NOT interactive.
```

14. Use `basename` and `dirname` to get filename and path from a full path.

```bash
#!/bin/bash

# Check if shell is interactive
directory="$(pwd)/test.sh"
echo "Current directory: $directory"

echo "File: $(basename $directory)"
echo "Path: $(dirname $directory)"
```
```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Current directory: /mnt/c/Users/yadav.deepak/Desktop/practise/test.sh
File: test.sh
Path: /mnt/c/Users/yadav.deepak/Desktop/practise
```

15. 🧑‍💼 **Real-time**: Create a bootstrap shell script that prints basic system info like hostname, IP, OS, shell.
```bash
#!/bin/bash

echo "Hostname: $(hostname)"
echo "IP Address: $(hostname -I | awk '{print $1}')"
echo "Operating System: $(uname -s)"
echo "Kernel Version: $(uname -r)"
echo "Shell Type: $SHELL"
```
```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Hostname: LG7G0DB3
IP Address: 172.25.99.183
Operating System: Linux
Kernel Version: 6.6.87.2-microsoft-standard-WSL2
Shell Type: /bin/bash
```
---

## ✅ **Module 2: Basic Shell Scripting – 15 Coding Questions**

1. Write a script to read your name and print "Welcome, \[name]".

```bash
#!/bin/bash

read -p "Enter your name: " name
if [ -z "$name" ]; then
  echo "No name provided. Exiting."
  exit 1
fi
echo "Hello, $name! Welcome to the script."
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Enter your name: 
No name provided. Exiting.
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Enter your name: Deepak
Hello, Deepak! Welcome to the script.
```

2. Define a local variable and print it

```bash
#!/bin/bash

name=$1
if [ -z "$name" ]; then
  echo "No name provided. Exiting."
  exit 1
fi
echo "Hello, $name! Welcome to the script."
```

<img width="918" height="153" alt="image" src="https://github.com/user-attachments/assets/39121415-3d6a-44ee-8fdf-3bd6f790fa9a" />


3. Export an environment variable and access it in a sub-shell.

<img width="1147" height="744" alt="image" src="https://github.com/user-attachments/assets/b9e5761b-b977-4390-aeb3-5519dd94db2a" />


4. Add two integer variables and print the result.

```bash
#!/bin/bash

a=$1
b=$2

c=$(( a + b ))

echo "The sum of $a and $b is: $c"
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh 2 3
The sum of 2 and 3 is: 5
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ 
```

5. Store a string in a variable and find its length.

```bash
#!/bin/bash

string="Hello, World!"
echo "Length of the string : ${#string} "
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Length of the string : 13 
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ 
```

6. Declare and access elements of an array.

```bash
#!/bin/bash

a=(1 2 3 4 5)
for i in "${a[@]}"; do
  echo "Element: $i"
done
echo "All elements: ${a[@]}"
echo "Number of elements: ${#a[@]}"
echo "First element: ${a[0]}"
echo "Last element: ${a[-1]}"
echo "Array indices: ${!a[@]}"
echo "Array as string: ${a[*]}"
echo "Array as string (with quotes): ${a[@]}"
echo "Array length using length operator: ${#a[*]}"
echo "Array length using length operator (with quotes): ${#a[@]}"
echo "Array elements in reverse order (using loop):"
for (( idx=${#a[@]}-1; idx>=0; idx-- )); do
  echo "Element in reverse: ${a[$idx]}"
done
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Element: 1
Element: 2
Element: 3
Element: 4
Element: 5
All elements: 1 2 3 4 5
Number of elements: 5  
First element: 1        
Last element: 5
Array indices: 0 1 2 3 4
Array as string: 1 2 3 4 5
Array as string (with quotes): 1 2 3 4 5
Array length using length operator: 5
Array length using length operator (with quotes): 5
Array elements in reverse order (using loop):
Element in reverse: 5
Element in reverse: 4
Element in reverse: 3
Element in reverse: 2
Element in reverse: 1
```

7. Write a script using single quotes and double quotes, showing difference.
``` Refer Module 1 notes ```
8. Read two inputs from the user and display their sum.

```bash
#!/bin/bash

read -p "Enter first number: " a
read -p "Enter second number: " b

c=$(( a + b ))

echo "The sum of $a and $b is: $c"
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Enter first number: 2
Enter second number: 3
The sum of 2 and 3 is: 5
```

9. Use backticks to store the output of `date` and print it.

```Refer notes```

10. Comment all lines in a script using `#`.

```Refer notes```

11. Write a script that returns 1 if a condition is false.

```bash
#!/bin/bash

read -p "Enter first number: " a
read -p "Enter second number: " b

c=$(( a + b ))

echo "The sum of $a and $b is: $c"

if (( c > 0 )); then
    echo "The result is positive."
   
else
    echo "The result is not positive."
    exit 1
fi      

```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh 
Enter first number: 2
Enter second number: 3
The sum of 2 and 3 is: 5
The result is positive.
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh 
Enter first number: -1
Enter second number: -2
The sum of -1 and -2 is: -3
The result is not positive.
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ 
```

12. Check the exit status of the `ls` command.

```bash
#!/bin/bash

ls1=$(ls /etc)  

echo "Status of last command 1: $?"

ls2=$(ls /nonexistent_directory 2>/dev/null)

echo "Status of last command 2: $?"

```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Status of last command 1: 0
Status of last command 2: 2
```

13. Accept a file name as input and display if it exists or not.

```bash
#!/bin/bash

read -p "Enter the path to the directory with filename: " dir_path
read -p "Enter the filename to search for: " file_name

found=0
while IFS= read -r file; do
    if [[ "$file" == "$file_name" ]]; then
        echo "Found: $file"
        found=1
        break
    fi
done < <(ls "$dir_path")

if [[ $found -eq 1 ]]; then
    echo "File '$file_name' exists in directory '$dir_path'."
else
    echo "File '$file_name' not found in directory '$dir_path'."
fi

```

```bash
#!/bin/bash

read -p "Enter the path to the directory with filename: " dir_path
read -p "Enter the filename to search for: " file_name

# List files and loop through each line
ls "$dir_path" | while IFS= read -r file; do
    if [[ "$file" == "$file_name" ]]; then
        echo "Found: $file"
    else
        echo "Not found: $file"
    fi
done

```

```bash
#!/bin/bash

read -p "Enter the path to the directory: " dir_path
read -p "Enter the filename to search for: " file_name

found=0
while IFS= read -r file; do
    if [[ "$(basename "$file")" == "$file_name" ]]; then
        echo "Found: $file"
        found=1
    fi
done < <(find "$dir_path" -type f)

if [[ $found -eq 0 ]]; then
    echo "File not found."
fi

```

``` Concepts ```

 > Understanding `<`, `< <(...)`, and `IFS` will make your Bash scripting much more powerful and reliable.

---

### ✅ `IFS` – Internal Field Separator

#### 📌 What it is:

* `IFS` is a **special shell variable** (not a keyword) used by Bash to **split strings** into words/tokens.

#### 🔧 Default value:

```bash
IFS=" \t\n"  # space, tab, newline
```

#### 🔄 When reading files:

If you don’t override `IFS`, Bash will split lines on spaces/tabs too — which may **break filenames** with spaces.

#### ✅ Usage in your script:

```bash
while IFS= read -r line; do ...
```

* `IFS=` → disables word splitting completely.
* `read -r` → disables interpretation of backslashes (`\`).
* ✅ This is **best practice** when reading lines or filenames reliably.

---

### ✅ `<` vs `< <(...)` vs `<<`

| Syntax          | Name                 | Use Case                                                                |
| --------------- | -------------------- | ----------------------------------------------------------------------- |
| `cmd < file`    | Input redirection    | Feed the contents of `file` as input to `cmd` or a loop                 |
| `cmd < <(...)`  | Process substitution | Feed the output of a command (like `find`) into another command or loop |
| `<<EOF ... EOF` | Here Document        | Provide multiline **inline input** in a script                          |

---

### 🔍 Examples

#### 1️⃣ `<` – Input from a file

```bash
while read line; do
    echo "$line"
done < myfile.txt
```

✅ Reads from a file line by line.

---

#### 2️⃣ `< <(...)` – Process substitution

```bash
while read line; do
    echo "$line"
done < <(ls /tmp)
```

✅ Takes **output** of `ls /tmp` and feeds it to the loop.

---

#### 3️⃣ `<<` – Here document

```bash
cat <<EOF
Hello Deepak
This is a test.
EOF
```

✅ Used when you want to pass **multiple lines of text** as input.

---

### 🔑 Summary

| Symbol     | Description                                  | Typical Use Case                                 |
| ---------- | -------------------------------------------- | ------------------------------------------------ |
| `< file`   | Input redirection                            | Read from a file                                 |
| `< <(...)` | **Process substitution**                     | Read from **command output**                     |
| `<<EOF`    | **Here document** (inline multiline content) | Simulate file input or feed data to a command    |
| `IFS`      | Word-splitting behavior for `read` etc.      | Set to empty (`IFS=`) to prevent unwanted splits |

---

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Enter the path to the directory with filename: /mnt/c/Users/yadav.deepak/Desktop/practise
Enter the filename to search for: sales.csv
Found: sales.csv
File 'sales.csv' exists in directory '/mnt/c/Users/yadav.deepak/Desktop/practise'.
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Enter the path to the directory with filename: /mnt/c/Users/yadav.deepak/Desktop/practise
Enter the filename to search for: abc.txt
File 'abc.txt' not found in directory '/mnt/c/Users/yadav.deepak/Desktop/practise'.
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$
```

14. Accept multiple inputs using `read -p` in a single line.

```bash
#!/bin/bash

read -p "Enter name and age (e.g., John 30): " name age
echo "Hello, $name! You are $age years old."
```

```bash
deepak@LG7G0DB3:/mnt/c/Users/yadav.deepak/Desktop/practise$ ./test.sh
Enter name and age (e.g., John 30): Deepak 25
Hello, Deepak! You are 25 years old.
```

15. 🧑‍💼 **Real-time**: Script that takes app name and port from user, and prints a simulated deployment message.

```Similar to above question```

---

## ✅ **Module 3: Conditional Statements – 15 Coding Questions**

1. Write a script to check if a number is positive, negative, or zero.

```bash
#!/bin/bash
read -p "Enter a number: " n
echo "You entered: $n"
if (( n < 0 )); then 
    echo "Negative number entered."
elif (( n == 0 )); then 
    echo "Zero entered."
else 
    echo "Positive number entered."
fi

```

```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter a number: 0
You entered: 0
Zero entered.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter a number: -1
You entered: -1
Negative number entered.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter a number: 2
You entered: 2
Positive number entered.
```

2. Check if a file exists using `-f`.
```bash
#!/bin/bash
read -p "Enter a file name: " file
if [[ -f $file ]]; then
    echo "File $file exists."
else
    echo "File $file does not exist."
fi

```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter a file name: test.sh
File test.sh exists.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter a file name: testt.sh
File testt.sh does not exist.
```

3. Check if a directory exists using `-d`.

```bash
#!/bin/bash
# This script checks if a given directory exists
read -p "Enter the directory: " dir

if [[ -d $dir ]]; then
    echo "Directory $dir exists."
else
    echo "Directory $dir does not exist."
fi

```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh
Enter the directory: /mnt/d/Study/Linux/shell Scripting/Scripts
Directory /mnt/d/Study/Linux/shell Scripting/Scripts exists.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the directory: /mnt/d/Study/Linux/shell Scripting/Scripts_Not_Exist
Directory /mnt/d/Study/Linux/shell Scripting/Scripts_Not_Exist does not exist.
```

4. Compare two strings for equality and inequality.

```bash
#!/bin/bash
# This script compares two strings entered by the user.
read -p "Enter the String 1: " str1
read -p "Enter the String 2: " str2

if [[ "$str1" == "$str2" ]]; then
    echo "The strings are equal."
else
    echo "The strings are not equal."
fi

```

```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the String 1: ABC
Enter the String 2: ABC
The strings are equal.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the String 1: ABC
Enter the String 2: CBA
The strings are not equal.
```
  
5. Compare two numbers using `-eq`, `-gt`, `-lt`.
```bash
#!/bin/bash
# This script compares two numbers
read -p "Enter the Num 1: " num1
read -p "Enter the Num 2: " num2

if [[ $num1 -eq $num2 ]]; then
    echo "Both numbers are equal."
elif [[ $num1 -gt $num2 ]]; then
    echo "Num 1 is greater than Num 2."
else
    echo "Num 2 is greater than Num 1."
fi

```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the Num 1: 23
Enter the Num 2: 12
Num 1 is greater than Num 2.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the Num 1: 11
Enter the Num 2: 32
Num 2 is greater than Num 1.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the Num 1: 11
Enter the Num 2: 11
Both numbers are equal.
```

6. Write a login script: if username == "admin", print "Welcome admin".
```bash
#!/bin/bash

read -p "Enter the name : " name

if [[ "$name" == "admin" ]]; then
    echo "Welcome, $name!"
else
    echo "Access denied."
fi
```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the name : admin
Welcome, admin!
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the name : Deepak
Access denied.
```

7. Use `[[ ... ]]` to test a string contains a substring.
```bash
#!/bin/bash

str="DevOps with Deepak"
[[ $str == *Deepak* ]] && echo "Found"
```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Found
```

8. Use `&&` to run a second command only if the first succeeds.

```bash
#!/bin/bash

str="DevOps with Deepak"
[[ $str == *Deepak* ]] && echo "Found"
[[ $str == *NotFound* ]] && echo " Not Found"
```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Found
```

9. Use `||` to provide fallback if a command fails.

```bash
#!/bin/bash

str="DevOps with Deepak"
[[ $str == *Deepak* ]] && echo "Found"
[[ $str == *NotFound* ]] || echo "Not Found"
```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Found
Not Found
```

10. Use `!` to reverse a condition in an if block.
```bash
#!/bin/bash

str="DevOps with Deepak"
if [[ $str == *Deepak* ]] ; then 
    echo "Found"
elif [[ $str != *DevOps* ]] ; then 
    echo "Not Found DevOps"
else
    echo "Nothing Found"
fi

```

```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Found
^Cepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ^C
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Nothing Found
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Not Found DevOps
```

11. Check if a file is readable and writable.

```bash
#!/bin/bash

if [[ -r testt.sh && -w test.sh ]]; then
    echo "The file test.sh is readable and writable."
else
    echo "The file test.sh is not readable or writable."
fi
```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
The file test.sh is readable and writable.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
The file test.sh is not readable or writable.
```

12. Write a script to compare two user-input numbers and print the larger.
```bash
#!/bin/bash

read -p "Enter the num1 : " num1
read -p "Enter the num2 : " num2

((( num1 > num2 )) && echo "Number1 $num1 is greater") || \
((( num1 < num2 )) && echo "Number2 $num2 is greater") || \
echo "Both numbers are equal"
```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the num1 : 11
Enter the num2 : 11
Both numbers are equal
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the num1 : 22
Enter the num2 : 11
Number1 22 is greater
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the num1 : 11
Enter the num2 : 22
Number2 22 is greater
```

13. Write a script to print a grade based on score using `if-elif-else`.
```bash
#!/bin/bash

read -p "Enter your score (0-100): " score

if [[ ! "$score" =~ ^[0-9]+$ ]]; then
    echo "Invalid input. Please enter a numeric score."
    exit 1

# Check if score is in the valid range
elif (( score < 0 || score > 100 )); then
    echo "Invalid score. Please enter a value between 0 and 100."
    exit 1

# Determine the grade based on the score
elif (( score >= 90 && score <= 100 )); then
    echo "Grade: A"
elif (( score >= 80 )); then
    echo "Grade: B"
elif (( score >= 70 )); then
    echo "Grade: C"
elif (( score >= 60 )); then
    echo "Grade: D"
else 
    echo "Grade: F"
fi

```

```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter your score (0-100): 
Invalid input. Please enter a numeric score.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter your score (0-100): 200
Invalid score. Please enter a value between 0 and 100.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter your score (0-100): 100
Grade: A
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter your score (0-100): 45
Grade: F
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter your
```
14. Use `case` statement to match input with options: start, stop, restart.
```bash
#!/bin/bash

read -p "Enter action (start | stop | restart): " action

case "$action" in
    start)
        echo "Service is starting..."
        ;;
    stop)
        echo "Service is stopping..."
        ;;
    restart)
        echo "Service is restarting..."
        ;;
    *)
        echo "Invalid action. Please enter start, stop, or restart."
        ;;
esac

```

```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter action (start | stop | restart): start
Service is starting...
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter action (start | stop | restart): restart
Service is restarting...
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter action (start | stop | restart): stop
Service is stopping...
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter action (start | stop | restart): WrongInput
Invalid action. Please enter start, stop, or restart.
```

15. 🧑‍💼 **Real-time**: Validate if a config file exists, is readable, and has a non-zero size.
```bash
#!/bin/bash

read -p "Enter the config file path: " config_file

if [[ -f "$config_file" && -r "$config_file" && -s "$config_file" ]]; then
    echo " '$config_file' exists, is a regular readable file, and is not empty."
else
    echo " File check failed:"
    [[ ! -f "$config_file" ]] && echo "   - File does not exist or is not a regular file."
    [[ -f "$config_file" && ! -r "$config_file" ]] && echo "   - File is not readable."
    [[ -f "$config_file" && -r "$config_file" && ! -s "$config_file" ]] && echo "   - File is empty."
fi

```
```bash
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the config file path: test.sh
 'test.sh' exists, is a regular readable file, and is not empty.
deepak@DeepakRK:/mnt/d/Study/Linux/shell Scripting/Scripts$ ./test.sh 
Enter the config file path: rest.sh
 File check failed:
   - File does not exist or is not a regular file.
```
| Flag | Meaning                                    | Applies To           |
| ---- | ------------------------------------------ | -------------------- |
| `-e` | File exists                                | File (any type)      |
| `-f` | File exists **and** is a regular file      | File                 |
| `-r` | File is readable                           | File                 |
| `-s` | File size is greater than zero (non-empty) | File                 |
| `-z` | String is empty                            | **String**, not file |

---

## ✅ **Module 4: Loops and Iterations – 15 Coding Questions**

1. Print numbers 1 to 10 using a `for` loop.
2. Print numbers 10 to 1 using a C-style `for ((...))` loop.
3. Loop over a list of names and print each.
4. Loop through an array and print elements.
5. Use a `while` loop to print numbers from 1 to 5.
6. Use an `until` loop to wait until a variable reaches 10.
7. Use `break` to exit a loop when number equals 5.
8. Use `continue` to skip printing number 3.
9. Loop through all files in current directory.
10. Loop through command output of `ls` and print file names.
11. Use a loop to create 5 empty files: file1.txt to file5.txt.
12. Print even numbers from 1 to 10 using a loop.
13. Sum of numbers 1 to 100 using loop.
14. Delete all `.tmp` files in current directory using loop.
15. 🧑‍💼 **Real-time**: Monitor a directory every 5 sec (use `while` + `sleep`) and print if new files are added.

---

## ✅ ✅ ✅ **Answers to All Coding Questions**

Here's the **continuation with all answers** to the 60 shell scripting coding questions, divided by module 👇

---

## ✅ **Module 1: Introduction to Shell and Bash – Answers**

```bash
#1
#!/bin/bash
echo "Hello DevOps"

#2
#!/bin/bash
echo "Shell: $SHELL"
echo "User: $USER"

#3
cat /etc/shells

#4
#!/bin/bash
pwd

#5
#!/bin/shh
echo "Testing invalid shebang"  # Will throw an error

#6
!!  # repeat last command (in terminal)

#7
#!/bin/bash
echo "Script Name: $0"
echo "Arguments: $@"

#8
#!/bin/bash
echo "Current Shell: $SHELL"

#9
#!/bin/bash
printenv

#10
alias ll='ls -l'
ll

#11
bash script.sh
./script.sh

#12
current_dir=$(pwd)
echo "Directory: $current_dir"

#13
[[ $- == *i* ]] && echo "Interactive" || echo "Non-Interactive"

#14
#!/bin/bash
path="/usr/bin/bash"
echo "File: $(basename $path)"
echo "Path: $(dirname $path)"

#15 (Real-time)
#!/bin/bash
echo "Hostname: $(hostname)"
echo "IP Address: $(hostname -I)"
echo "OS: $(uname -a)"
echo "Shell: $SHELL"
```

---

## ✅ **Module 2: Basic Shell Scripting – Answers**

```bash
#1
read -p "Enter your name: " name
echo "Welcome, $name"

#2
myvar="Deepak"
echo $myvar

#3
export MYENV=123
bash -c 'echo "MYENV=$MYENV"'

#4
a=5; b=10
echo "Sum = $((a + b))"

#5
str="Shell"
echo "Length = ${#str}"

#6
arr=(one two three)
echo "${arr[1]}"

#7
echo 'This is $HOME'     # prints literal
echo "This is $HOME"     # expands variable

#8
read -p "Enter two numbers: " x y
echo "Sum = $((x + y))"

#9
now=`date`
echo "Now = $now"

#10
# This is a comment
echo "Script running"

#11
return 1  # inside function only
# or use `exit 1`

#12
ls /tmp
echo "Exit status: $?"

#13
read -p "Enter filename: " f
[[ -f "$f" ]] && echo "Exists" || echo "Not found"

#14
read -p "Enter name and city: " name city
echo "$name is from $city"

#15 (Real-time)
read -p "App name: " app
read -p "Port: " port
echo "Deploying $app on port $port..."
```

---

## ✅ **Module 3: Conditional Statements – Answers**

```bash
#1
read -p "Enter number: " n
if ((n > 0)); then echo "Positive"
elif ((n < 0)); then echo "Negative"
else echo "Zero"; fi

#2
[ -f file.txt ] && echo "File exists"

#3
[ -d /etc ] && echo "Directory exists"

#4
str1="abc"; str2="xyz"
[ "$str1" = "$str2" ] || echo "Not equal"

#5
a=10; b=20
[ $a -gt $b ] && echo "a > b" || echo "a <= b"

#6
read -p "Username: " u
if [ "$u" = "admin" ]; then echo "Welcome admin"; fi

#7
str="DevOps with Deepak"
[[ $str == *Deepak* ]] && echo "Found"

#8
mkdir test && cd test

#9
ls nothere.txt || echo "Fallback: file not found"

#10
[ ! -f abc.txt ] && echo "File not present"

#11
[ -r myfile.txt ] && [ -w myfile.txt ] && echo "RW OK"

#12
read -p "Enter two numbers: " a b
((a > b)) && echo "$a is larger" || echo "$b is larger"

#13
read -p "Score: " s
if ((s >= 90)); then echo "Grade A"
elif ((s >= 75)); then echo "Grade B"
else echo "Grade C"; fi

#14
read -p "Action (start/stop): " action
case $action in
start) echo "Starting...";;
stop) echo "Stopping...";;
*) echo "Invalid";;
esac

#15 (Real-time)
conf="app.conf"
if [[ -f $conf && -s $conf && -r $conf ]]; then
  echo "$conf is valid"
else
  echo "Check config file"
fi
```

---

## ✅ **Module 4: Loops and Iterations – Answers**

```bash
#1
for i in {1..10}; do echo $i; done

#2
for ((i=10;i>=1;i--)); do echo $i; done

#3
for name in Alice Bob Charlie; do echo $name; done

#4
arr=(one two three)
for item in "${arr[@]}"; do echo $item; done

#5
i=1
while [ $i -le 5 ]; do echo $i; ((i++)); done

#6
i=1
until [ $i -gt 10 ]; do echo $i; ((i++)); done

#7
for i in {1..10}; do
  [ $i -eq 5 ] && break
  echo $i
done

#8
for i in {1..5}; do
  [ $i -eq 3 ] && continue
  echo $i
done

#9
for file in *; do echo $file; done

#10
for file in $(ls); do echo $file; done

#11
for i in {1..5}; do touch file$i.txt; done

#12
for i in {1..10}; do
  [ $((i%2)) -eq 0 ] && echo $i
done

#13
sum=0
for i in {1..100}; do ((sum+=i)); done
echo "Total = $sum"

#14
for f in *.tmp; do rm -f "$f"; done

#15 (Real-time)
prev=$(ls | wc -l)
while true; do
  sleep 5
  now=$(ls | wc -l)
  [ $now -ne $prev ] && echo "New file(s) detected!"
  prev=$now
done
```

---

