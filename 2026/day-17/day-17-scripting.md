# Day 17 - Shell Scripting: Loops, Arguments & Error Handling

## Overview
This document summarizes the learning journey through shell scripting covering loops, command-line arguments, package installation, and error handling.

---

## Task 1: For Loops

### Script 1a: for_loop.sh
**Purpose**: Loop through a list of fruits and print each one

```bash
#!/bin/bash

#task 1(1)   ====> Loops through a list of 5 fruits and prints each one

list=("apple","moango","banana","grapes","orange")

for fruit in $list;
do
	echo "$fruit"
done
```

**Output**:
```
apple
moango
banana
grapes
orange
```

---

### Script 1b: count.sh
**Purpose**: Print numbers 1 to 10 using a for loop

```bash
#!/bin/bash
#Task 1 (2) ============> Prints numbers 1 to 10 using a for loop

for number in {1..10};
do
	echo "$number"

done
```

**Output**:
```
1
2
3
4
5
6
7
8
9
10
```

---

## Task 2: While Loops

### Script: countdown.sh
**Purpose**: Take a number from user and countdown to 0

```bash
#!/bin/bash
# task 2 ===> Takes a number from the user,Counts down to 0 using a while loop,Prints "Done!" at the end

read -p "enter the number: " number

while [ $number -gt 0 ];
do
	echo "$number"
       	((number --))

done	
echo "Done!"
```

**Output** (Example with input 5):
```
enter the number: 5
5
4
3
2
1
Done!
```

**Key Concept**: The `while` loop continues execution as long as the condition is true. We decrement the counter using `((number --))` and print "Done!" after completion.

---

## Task 3: Command-Line Arguments

### Script 3a: greet.sh
**Purpose**: Accept a name as argument and print greeting

```bash
#!/bin/bash
#
# -z: checks if the length of the string is zero. If it is zero, it returns true; otherwise, it returns false.
if [ -z $1 ];
then
	echo "Usage: ./greet.sh <name>"
else
	echo "Hello, $1 "
fi
```

**Output Examples**:
```
# Without argument
$ ./greet.sh
Usage: ./greet.sh <name>

# With argument
$ ./greet.sh DevOps
Hello, DevOps
```

---

### Script 3b: args_demo.sh
**Purpose**: Demonstrate command-line argument variables

```bash
#!/bin/bash

echo "script name: $0 "
echo "number of arguments: $#"
echo "all arguments: $@"
```

**Output** (Example):
```
$ ./args_demo.sh arg1 arg2 arg3
script name: ./args_demo.sh
number of arguments: 3
all arguments: arg1 arg2 arg3
```

**Key Concepts**:
- `$0` = Script name
- `$#` = Total number of arguments
- `$@` = All arguments as individual items

---

## Task 4: Install Packages via Script

### Script: install_packages.sh
**Purpose**: Check and install packages with root privilege verification

```bash
#!/bin/bash
#

# This script checks if the user is root 
if [ $EUID -ne 0 ]
then
	echo "run as root user"
	exit 1
fi

packages=("nginx" "curl" "wget")

for package in ${packages[@]}
do
	echo "checking package ...."

	dpkg -s $package >/dev/null 2>&1
#   $? is a special variable in bash that holds the exit status of the last executed command. 
	if [ $? -eq 0 ]
	then
		echo "alrerady installed ...."
	else
		echo "not installed"
		echo "installing"
		sudo apt-get install -y $package
	fi
done
```

**Output** (Example):
```
checking package ....
alrerady installed ....
checking package ....
not installed
installing
[Installation output...]
```

**Key Concepts**:
- `$EUID` = Effective User ID (0 = root)
- `dpkg -s` = Check if package is installed
- `$?` = Exit status of last command (0 = success, non-zero = failure)
- Loops through array and conditionally installs packages

---

## Task 5: Error Handling

### Script: safe_script.sh
**Purpose**: Implement error handling with exit-on-error and error operators

```bash
#!/bin/bash

set -e

mkdir -p /tmp/devops-test || { echo "Failed to create directory"; exit 1; }

cd /tmp/devops-test || { echo "Failed to navigate"; exit 1; }

touch test.txt || { echo "Failed to create file"; exit 1; }

echo "All steps completed successfully"
```

**Output** (Success):
```
All steps completed successfully
```

**Output** (If directory creation fails):
```
Failed to create directory
```

**Key Concepts**:
- `set -e` = Exit immediately if any command exits with non-zero status
- `||` operator = Execute right side if left side fails
- Error handling prevents partial script execution
- `-p` flag in mkdir creates parent directories if needed

---

## What I Learned - 3 Key Points

### 1. **Loop Control & Iteration**
   - **For loops** are ideal for iterating over lists, number ranges, and arrays
   - **While loops** are best for conditional iterations where you don't know the count in advance
   - Syntax: `for item in list; do ... done` and `while [ condition ]; do ... done`
   - Both can be controlled with `break` and `continue` statements

### 2. **Command-Line Arguments & Script Parameters**
   - Arguments allow scripts to be flexible and reusable
   - `$0` = script name, `$1` = first arg, `$#` = count, `$@` = all args
   - Always validate arguments before using them (check if they exist with `-z`)
   - Arguments enable creating interactive and dynamic shell scripts

### 3. **Error Handling & Robustness**
   - `set -e` makes scripts fail fast by exiting on first error
   - The `||` operator provides immediate error handling for specific commands
   - Check command exit status with `$?` (0 = success, others = failure)
   - Root privilege checking with `$EUID` prevents permission errors
   - Proper error handling prevents partial script execution and data inconsistency

---

## Summary of Scripts Created
| Script | Purpose | Key Feature |
|--------|---------|------------|
| `for_loop.sh` | Loop through fruits | Array iteration with for loop |
| `count.sh` | Print 1-10 | Numeric range iteration |
| `countdown.sh` | Count down from input | While loop with user input |
| `greet.sh` | Greet with name argument | Argument validation |
| `args_demo.sh` | Show special variables | `$0`, `$#`, `$@` demonstration |
| `install_packages.sh` | Install packages safely | Root check + package manager |
| `safe_script.sh` | Safe directory operations | Error handling with exit codes |

---

## Conclusion
Through these 5 tasks, I've mastered the core concepts of shell scripting: iteration control, parameter handling, and robust error management. These skills are essential for writing production-ready DevOps scripts that are reliable and maintainable.

---

`#90DaysOfDevOps` `#DevOpsKaJosh` `#TrainWithShubham` `#ShellScripting` `#Linux` `#DevOps`
