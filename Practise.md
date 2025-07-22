# Bash Scripting Practise Questions

Here's a **module-wise collection of 15 shell scripting coding questions** per module (no theory), followed by **answers at the end**. I’ve also added a few **real-world/practical scripting questions** in each section.

---

## ✅ **Module 1: Introduction to Shell and Bash – 15 Coding Questions**

1. Write a script to print "Hello DevOps" using `#!/bin/bash`.
2. Create a script that prints your current shell and username.
3. Print the list of all shells available in the system.
4. Create a script that prints the current directory using a command shortcut.
5. Create a script with incorrect shebang and observe behavior.
6. Use history expansion to repeat the last command in a script.
7. Display script name and number of arguments passed.
8. Write a script to display current shell type using `$SHELL`.
9. Show all environment variables from a script.
10. Use alias in a script to replace `ls -l` with `ll`.
11. Create a script and run it with `bash script.sh` and `./script.sh`. Observe differences.
12. Store the output of `pwd` in a variable and print it.
13. Write a script to check whether the current shell is interactive or not.
14. Use `basename` and `dirname` to get filename and path from a full path.
15. 🧑‍💼 **Real-time**: Create a bootstrap shell script that prints basic system info like hostname, IP, OS, shell.

---

## ✅ **Module 2: Basic Shell Scripting – 15 Coding Questions**

1. Write a script to read your name and print "Welcome, \[name]".
2. Define a local variable and print it.
3. Export an environment variable and access it in a sub-shell.
4. Add two integer variables and print the result.
5. Store a string in a variable and find its length.
6. Declare and access elements of an array.
7. Write a script using single quotes and double quotes, showing difference.
8. Read two inputs from the user and display their sum.
9. Use backticks to store the output of `date` and print it.
10. Comment all lines in a script using `#`.
11. Write a script that returns 1 if a condition is false.
12. Check the exit status of the `ls` command.
13. Accept a file name as input and display if it exists or not.
14. Accept multiple inputs using `read -p` in a single line.
15. 🧑‍💼 **Real-time**: Script that takes app name and port from user, and prints a simulated deployment message.

---

## ✅ **Module 3: Conditional Statements – 15 Coding Questions**

1. Write a script to check if a number is positive, negative, or zero.
2. Check if a file exists using `-f`.
3. Check if a directory exists using `-d`.
4. Compare two strings for equality and inequality.
5. Compare two numbers using `-eq`, `-gt`, `-lt`.
6. Write a login script: if username == "admin", print "Welcome admin".
7. Use `[[ ... ]]` to test a string contains a substring.
8. Use `&&` to run a second command only if the first succeeds.
9. Use `||` to provide fallback if a command fails.
10. Use `!` to reverse a condition in an if block.
11. Check if a file is readable and writable.
12. Write a script to compare two user-input numbers and print the larger.
13. Write a script to print a grade based on score using `if-elif-else`.
14. Use `case` statement to match input with options: start, stop, restart.
15. 🧑‍💼 **Real-time**: Validate if a config file exists, is readable, and has a non-zero size.

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

