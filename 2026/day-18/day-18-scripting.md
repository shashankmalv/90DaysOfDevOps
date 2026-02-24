# Day 18 – Shell Scripting: Functions & All That Good Stuff

So today was all about writing cleaner, reusable shell scripts. Got introduced to functions properly, learned about strict mode (which honestly saves your butt in production), and how to keep variables from leaking all over the place.

Started with basic stuff and gradually built up to creating a full system info script. The progression made a lot of sense - each task built on what I learned before.

---

## Task 1: Basic Functions

**What I had to do:** Create two simple functions - one to greet someone by name, another to add two numbers. Pretty straightforward start.

**Here's what I wrote:**
```bash
#!/bin/bash
# Task 1: Basic Functions

function greet(){
  local name=$1
  echo "Hello, $name!"
}

function add(){
  local num1=$1
  local num2=$2
  local sum=$(( num1 + num2 ))
  echo "Sum of two numbers: $sum"
}

greet "Shashank"
add 5 3
```

**Output when I ran it:**
```
Hello, Shashank!
Sum of two numbers: 8
```

**What clicked for me:** 

I realized functions in bash are just chunks of code you write once and then call by name. The `$1` and `$2` thing was new - that's how you access arguments passed to the function. So when I call `greet "Shashank"`, inside the function `$1` becomes "Shashank".

Also messed up the arithmetic at first - was treating it like Python. Have to use `$(( num1 + num2 ))` not just `$num1+$num2`. The `local` keyword kept variables from accidentally becoming global which is good practice.

---

## Task 2: Functions with Return Values

**Goal:** Actually pull some system info using functions and organize it nicely.

**My code:**
```bash
#!/bin/bash
# Task 2: Functions with Return Values

function check_disk(){
  df -h | grep "/$"
}

function check_memory(){
  free -h
}

# Main section
echo "=== System Health Check ==="
echo ""
echo "--- Disk Usage (/) ---"
check_disk
echo ""
echo "--- Memory Usage ---"
check_memory
```

**What it shows:**
```
=== System Health Check ===

--- Disk Usage (/) ---
/dev/sda1       50G   20G   30G  40% /

--- Memory Usage ---
              total        used        free      shared  buff/cache   available
Mem:           15Gi       3.5Gi       8Gi       200Mi       3.5Gi       11Gi
```

**This is where it got interesting:** 

Each function calls a real system command (`df -h`, `free -h`) and outputs the result directly. The `df -h | grep "/$"` line filters the disk output to show only the root partition - that was cool because it combines two commands.

The pipe character `|` is basically saying "take the output from the left and feed it to the right." So `df -h` shows all filesystems, then `grep "/$"` filters to only the root one. Made the output much cleaner.

Adding headers before each section makes it way more readable than just dumping output.

---

## Task 3: Strict Mode - The Game Changer

**What this was about:** Learning `set -euo pipefail` - honestly the most important thing today.
```bash
#!/bin/bash

# Enable strict mode
set -euo pipefail

echo "Strict mode enabled"

#  Using undefined variable (set -u demo)
echo "Value of name is: $name"

# Command failure demo (set -e demo)
mkdir /root/test-folder

#  Pipe failure demo (set -o pipefail demo)
cat missingfile.txt | grep "hello"

echo "Script completed"
```

**Why this matters:**

The thing that really hit me is that without strict mode, a script can silently fail and you won't even know. That's dangerous. Like imagine a backup script fails to copy files but then deletes the originals - boom, data gone.

Here's what each part does:

**`set -e`** - If something goes wrong, stop right there. 
Would be like: backup fails → script stops here and never deletes anything. Keeps cascading failures from happening.

**`set -u`** - If you reference a variable that doesn't exist, stop.
Catches typos. So if I accidentally write `$MY_VAR` instead of `$MY_VER`, the script errors out instead of silently using an empty string.

**`set -o pipefail`** - If any command in a chain fails, the whole thing fails.
This one's sneaky. Normally if you do `cat file.txt | grep "pattern" | sort`, only the exit code of `sort` matters even if `grep` failed. With pipefail, you catch the grep failure too.

Running them all together at the start of every script is become my new habit.

---

## Task 4: Local Variables (The Scope Thing)

---

## Task 4: Local Variables

**The concept:**

By default, variables in bash are global. That sucks because if two functions accidentally use the same variable name, they mess with each other. Using `local` fixes that.

**Here's my code:**
```bash
#!/bin/bash
#
#
#
function demo_local(){
	#local variable
	local loc_var=56
	echo "value loc_var=$loc_var"
}

demo_local

#local variable is not accessible outside the function
echo "value loc_var=$loc_var"

# global variable
loc_var=100
echo "value loc_var=$loc_var"
```

**What happened when I ran it:**
```
value loc_var=56
value loc_var=
value loc_var=100
```

**The walkthrough:**

First call shows 56 because we're inside the function with the local variable. Second echo is empty because we're trying to print a variable that only existed inside the function. Then we create a global one and it prints 100.

This is the lightbulb moment - if I don't use `local`, that variable sticks around in the whole script and could cause problems later if another function uses the same name. With `local`, it's protected.

It's such a simple keyword but makes such a difference for avoiding accidental bugs.

---

## Task 5: System Info Reporter - Putting It All Together

---

## Task 5: Build a Script — System Info Reporter

**What the task wanted:** Write a script that shows system info using functions. Include hostname, OS, uptime, disk usage, memory, and top CPU hogs.

**My final version:**
```bash
#!/bin/bash

set -euo pipefail

# Function to print hostname and OS info
print_system_info() {
    echo "===== Hostname & OS Info ====="
    echo "Hostname: $(hostname)"
    echo "OS: $(uname -a)"
    echo
}

# Function to print uptime
print_uptime() {
    echo "===== Uptime ====="
    uptime
    echo
}

# Function to print top 5 disk usage by size
print_disk_usage() {
    echo "===== Disk Usage (Top 5) ====="
    df -h | head -n 5
    echo
}

# Function to print memory usage
print_memory_usage() {
    echo "===== Memory Usage ====="
    free -h
    echo
}

# Function to print top 5 CPU consuming processes
print_top_cpu() {
    echo "===== Top 5 CPU Processes ====="
    ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6
    echo
}

# Main function
main() {
    print_system_info
    print_uptime
    print_disk_usage
    print_memory_usage
    print_top_cpu
}

# Call main
main
```

### Expected Output:
```
===== Hostname & OS Info =====
Hostname: mycomputer
OS: Linux mycomputer 5.10.0 #1 SMP x86_64 GNU/Linux

===== Uptime =====
 10:45:32 up 5 days, 3:22,  2 users,  load average: 0.45, 0.52, 0.48

===== Disk Usage (Top 5) =====
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   30G  40% /
tmpfs           7.5G     0  7.5G   0% /dev/shm

===== Memory Usage =====
              total        used        free      shared  buff/cache   available
Mem:           15Gi       3.5Gi       8Gi       200Mi       3.5Gi       11Gi

===== Top 5 CPU Processes =====
    PID COMM             %CPU
    545 chrome            12.5
    678 node             8.3
    123 bash             2.1
```

### What I Learned:
1. **Modular function design:** Each function has one clear responsibility
2. **Orchestration pattern:** `main()` function calls all others in the right order
3. **Error safety first:** `set -euo pipefail` on line 3 protects the entire script
4. **Command substitution:** `$(hostname)` and `$(uname -a)` inject command output directly
5. **Filtering output:** `head -n 5` limits output, pipes chain commands together
6. **Professional formatting:** Headers and blank lines make output readable
7. **Real-world applicability:** This pattern is used in actual DevOps monitoring scripts

---

## 🎯 Three Key Takeaways

### **1. Functions Make Code Reusable**
Instead of writing the same commands multiple times, functions let you write once and call many times. This follows the DRY principle (Don't Repeat Yourself).

**Before (Messy):**
```bash
echo "Checking disk..."
df -h | grep "/$"
echo "Checking disk again..."
df -h | grep "/$"
```

**After (Clean):**
```bash
check_disk() { df -h | grep "/$"; }
echo "Checking disk..."
check_disk
echo "Checking disk again..."
check_disk  # Reuse!
```

### **2. `set -euo pipefail` Prevents Disasters**
In production scripts (deployments, backups, system management), one silent failure can cause catastrophic data loss. Strict mode makes scripts fail **loudly and immediately** instead of silently continuing.

**Always start with:**
```bash
#!/bin/bash
set -euo pipefail
```

### **3. `local` Variables Keep Code Safe**
Using `local` in functions prevents variables from leaking into the global namespace. This makes functions self-contained, testable, and less likely to have unexpected side effects.

**Good practice:**
```bash
function calculate() {
    local result=$(( $1 + $2 ))
    echo "$result"
}
# result doesn't exist here - safe! ✅
```

---

## 📊 Skills Achieved

- ✅ Write functions with proper bash syntax
- ✅ Pass and receive arguments in functions
- ✅ Use local variables for code safety
- ✅ Execute system commands within functions
- ✅ Implement strict mode for error handling
- ✅ Understand all three `set` flags (`e`, `u`, `pipefail`)
- ✅ Build production-quality scripts with modular design
- ✅ Format output professionally
- ✅ Use command substitution and piping
- ✅ Combine multiple concepts into complex scripts

---

## 🚀 Real-World Applications

These concepts are used daily in DevOps for:
- **Deployment scripts** - Safe, automated deployments
- **System monitoring** - Collect and report system statistics
- **Backup automation** - Reliable, fail-safe backups
- **Log analysis** - Process and filter logs efficiently
- **Infrastructure management** - Manage cloud resources with confidence
- **Continuous Integration/Deployment** - Automated testing and deployment pipelines

---

**Status: ✅ COMPLETED - All tasks finished with comprehensive understanding!**

---

**Tags:** `#90DaysOfDevOps` `#DevOpsKaJosh` `#TrainWithShubham` `#shell-scripting` `#bash` `#functions` `#strict-mode` `#local-variables` `#devops` `#scripting-best-practices` `#error-handling` `#system-administration` `#linux`
