# Day 16 – Shell Scripting Basics

## Overview

Today I started learning the fundamentals of Shell Scripting.  
The focus was on understanding how scripts work, how to make them executable, and how to add logic and interaction inside scripts.

This day helped me understand how automation begins at the command line level.

---

# Task 1 – Understanding Shebang & First Script

I created my first shell script that prints:

Hello, DevOps!

The most important thing I learned here was the role of the **shebang**:

#!/bin/bash

## What I Understood

- The shebang tells the system which interpreter should execute the script.
- Without it, the script may run using the system’s default shell.
- This can cause unexpected behavior if the script uses Bash-specific features.
- A script must be made executable using `chmod +x`.

## Why It Is Important

In DevOps, scripts run on different servers and environments.  
The shebang ensures consistency across systems.

---

# Task 2 – Variables and Quotes

I worked with variables to store:
- My name
- My role

Then printed them using `echo`.

## What I Understood

- Variables are declared without spaces around `=`.
- `$VARIABLE_NAME` is used to access a variable’s value.
- Double quotes allow variable expansion.
- Single quotes treat variables as plain text.

Example understanding:
- `'Hello $NAME'` → prints literal text
- `"Hello $NAME"` → prints expanded value

## Why It Is Important

Variables make scripts dynamic.  
Instead of hardcoding values, we can reuse scripts in different environments.

This is useful in:
- Environment configurations
- Deployment automation
- CI/CD pipelines

---

# Task 3 – User Input with `read`

I created a script that takes user input and prints a personalized message.

## What I Understood

- `read` allows interactive input.
- `-p` displays a prompt message.
- User input can be stored in variables.

## Why It Is Important

Interactive scripts are useful when:
- Confirming deployments
- Asking for configuration values
- Creating setup scripts
- Writing backup or maintenance tools

This makes scripts more flexible and user-friendly.

---

# Task 4 – If-Else Conditions

I created scripts that:
- Check whether a number is positive, negative, or zero
- Check whether a file exists

## What I Understood

- `if [ condition ]; then` starts a condition block.
- `elif` allows multiple conditions.
- `fi` ends the block.
- `-gt`, `-lt` are numeric comparison operators.
- `-f` checks if a file exists.

## Why It Is Important

Conditional logic allows scripts to make decisions.

In real-world DevOps scenarios, this is used for:
- Checking service status
- Validating configurations
- Running different steps based on environment
- Preventing failures before executing commands

---

# Task 5 – Combining Everything (Service Check Script)

I created a script that:
- Stores a service name in a variable
- Asks the user whether to check its status
- Prints whether the service is active or not

## What I Understood

- How to combine variables, input, and conditions together
- How to capture command output into a variable
- How to create real-world automation logic

## Why It Is Important

Service monitoring is a common DevOps task.  
Being able to check service status programmatically is useful for:

- Monitoring scripts
- Automated recovery
- Deployment validation
- Health checks in production systems

---

# Key Concepts Learned

- Shebang ensures correct interpreter usage
- Variables store reusable data
- Quotes affect variable expansion
- `read` enables interactive scripting
- `if-else` enables decision-making
- File and service checks are practical automation tools

---

# My Takeaway

Today I realized that shell scripting is not just about running commands.  
It is about creating automation with logic.

These fundamentals are essential for:
- Infrastructure automation
- CI/CD pipelines
- Server management
- Troubleshooting systems

---

## Tags

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham  
#ShellScripting  
#Linux  
#Automation  
#DevOpsJourney