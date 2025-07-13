# **Comprehensive Bash Scripting syllabus tailored for a DevOps Engineer**
---

## 🧾 **Bash Scripting Syllabus for DevOps Engineers**

### 🟢 **Module 1: Introduction to Shell and Bash**

* What is Shell and Bash?
* Bash vs Other Shells (sh, zsh, etc.)
* Interactive vs Non-Interactive Shell
* Shebang (`#!/bin/bash`)
* Script structure & execution
* Bash command line shortcuts

---

### 🟡 **Module 2: Basic Shell Scripting**

* Printing & echo statements
* Variables (local & environment)
* Data types (strings, integers, arrays)
* Quotes (single `'`, double `"`, backticks \`\`)
* Comments & documentation in scripts
* `read` input from user
* `exit`, `return` and exit status

---

### 🟢 **Module 3: Conditional Statements**

* `if`, `else`, `elif`
* `test` command and `[ ]`, `[[ ]]`
* Logical operators (`&&`, `||`, `!`)
* File condition checks (`-f`, `-d`, `-r`, etc.)
* String and integer comparisons

---

### 🟡 **Module 4: Loops and Iterations**

* `for` loop (C-style & list-based)
* `while` loop
* `until` loop
* `break` and `continue`
* Looping over files, command output, arrays

---

### 🟢 **Module 5: Functions**

* Creating and using functions
* Function arguments and return values
* Global vs Local variables
* Reusability of functions in multiple scripts

---

### 🟡 **Module 6: Working with Files and Text**

* File redirection (`>`, `>>`, `<`)
* Piping (`|`)
* Reading files line by line
* Creating, renaming, copying, deleting files
* String manipulation (`cut`, `awk`, `sed`)
* Search with `grep`, `egrep`
* Regular expressions (basic + extended)

---

### 🟢 **Module 7: Arrays and Associative Arrays**

* Defining arrays
* Looping through arrays
* Associative arrays (name=>value)
* Array slicing and indexing

---

### 🟡 **Module 8: Advanced Bash Topics**

* Command-line arguments (`$1`, `$@`, `$#`)
* `getopts` for parsing flags
* Exit status & error handling
* Trapping signals with `trap`
* Scheduling with `cron` & `at`
* Logging best practices
* Colored outputs

---

### 🟢 **Module 9: DevOps-Specific Use Cases**

* Automating user and group creation
* Log rotation & log monitoring
* Script to monitor disk, memory, CPU usage
* Backup and restore automation
* Docker container health checks via script
* Interacting with REST APIs using `curl` in bash
* Automating package installations (yum/apt)

---

### 🟡 **Module 10: Integration with DevOps Tools**

* Using bash with:

  * **Jenkins** (as part of build/test scripts)
  * **Git hooks** (pre-commit, post-commit)
  * **Dockerfile entrypoints**
  * **Ansible local shell tasks**
  * **Terraform external data sources**
  * **Kubernetes** (automation using `kubectl`)

---

### 🟢 **Module 11: Security and Best Practices**

* Secure handling of passwords & secrets
* Avoiding command injection
* Using `set -euo pipefail` for safety
* Idempotent scripting practices
* Version-controlling scripts (with Git)
* Script documentation & linting (`shellcheck`)

---

### 🟡 **Module 12: Projects and Practice**

* **Project 1:** Linux Resource Monitor Script (CPU, memory, disk)
* **Project 2:** Jenkins Job trigger script with status notification
* **Project 3:** Backup and rotate logs from `/var/log/`
* **Project 4:** EC2 instance health checker using AWS CLI
* **Project 5:** Git repository scanner for secrets & large files

---
