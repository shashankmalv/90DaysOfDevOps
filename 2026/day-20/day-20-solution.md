# Day 20 Solution – Bash Scripting Challenge: Log Analyzer and Report Generator

## Script Code

```bash
#!/bin/bash

# Check if argument provided
if [ $# -eq 0 ]; then
    echo "Usage: ./log_analyser.sh <log_file>"
    exit 1
fi

log_file="$1"

# Check if file exists
if [ ! -f "$log_file" ]; then
    echo "Error: File '$log_file' does not exist."
    exit 1
fi

echo "File '$log_file' exists and is ready for analysis."

report_date=$(date '+%d-%m-%Y')
report_file="log_report_${report_date}.txt"

total_line(){
    wc -l $log_file
}

error_count() {
    grep -c "ERROR" "$log_file"
}

critical_count(){
    echo "--- Last 5 Critical Errors ---"
    grep -n "CRITICAL" "$log_file" | head -n 5 | while IFS=: read -r line content; do
        echo "Line $line: $content"
    done
}

function top_error_message(){
    echo "--- Top 5 Error Messages ---"
    grep "ERROR" $log_file | awk '{$3=""; print}' | sort | uniq -c | sort -rn | head -5
}

function Summary_Report(){
    {
    echo "" 
    echo "--- Summary Report ---"
    echo "" 
   
    echo "Report Date: $report_date"
    echo ""
    echo "$report_file"
    echo ""
    echo "total line in tog file: $toal_line"
    echo "$(error_count)"
    echo ""
    echo "Total number of CRITICAL messages: $(critical_count)"
    echo ""
    echo "Top 5 ERROR messages: $(top_error_message)"
    } > "$report_file"
}

archive_log() {

    local archive_dir="archive"

    if [ ! -d "$archive_dir" ]; then
        mkdir -p "$archive_dir"
        echo "Archive directory created."
    fi

    mv "$log_file" "$archive_dir/"
    echo "Log file moved to $archive_dir/ successfully."
}
    



main() {
    
    Summary_Report
    archive_log
}

main
```

---

## What I Learned from Each Task

### Task 1: Input and Validation
- Learned how to use `$#` to check the number of command-line arguments
- Understood the importance of input validation before processing
- Used `[ ! -f "$log_file" ]` to check if a file exists
- Learned proper error handling with `exit 1` for script termination

### Task 2: Error Count
- Learned to use `grep -c` flag to count occurrences of a pattern
- Understood how to search for multiple keywords (ERROR or Failed) in log files
- Practiced creating reusable functions in bash scripts

### Task 3: Critical Events
- Learned to use `grep -n` to display line numbers along with matching lines
- Used `head -n 5` to limit output to the first 5 matches
- Practiced parsing grep output using `IFS` (Internal Field Separator) and `read` command
- Learned how to format output with custom messages

### Task 4: Top Error Messages
- Learned to chain multiple commands using pipes (`|`)
- Used `awk` to manipulate and remove specific fields from log entries
- Applied `sort` to organize data alphabetically
- Used `uniq -c` to count unique occurrences
- Applied `sort -rn` for reverse numerical sorting
- Used `head -5` to get top 5 results
- Understood the power of combining Unix utilities for data analysis

### Task 5: Summary Report
- Learned to use `date` command with format specifiers (`+%d-%m-%Y`)
- Practiced redirecting output to a file using `>` operator
- Created structured reports with multiple sections
- Learned to call functions and capture their output in a report

### Task 6: Archive Processed Logs
- Learned to check if a directory exists using `[ ! -d "$archive_dir" ]`
- Used `mkdir -p` to create directories (with parent directories if needed)
- Practiced moving files with `mv` command
- Understood the importance of organizing processed files

---

## Commands and Tools Used

- `grep`: Search for patterns in files
  - `-c`: Count matching lines
  - `-n`: Show line numbers
- `awk`: Text processing and field manipulation
- `sort`: Sort lines of text
  - `-r`: Reverse order
  - `-n`: Numerical sort
- `uniq -c`: Count unique occurrences
- `head`: Display first N lines
- `wc -l`: Count lines in a file
- `date`: Display or format date/time
- `mv`: Move or rename files
- `mkdir -p`: Create directories recursively
- Bash conditionals: `if`, `[ ]`, `[[ ]]`
- Command-line arguments: `$#`, `$1`
- Functions in bash
- Pipes (`|`) for chaining commands
- Output redirection (`>`)

---

## Key Takeaways

1. **Input Validation is Critical**: Always validate user inputs and file existence before processing to prevent runtime errors and provide clear feedback to users.

2. **Unix Philosophy - Do One Thing Well**: By combining simple tools like `grep`, `awk`, `sort`, and `uniq`, we can build powerful data analysis pipelines. Each tool does one thing well, and piping them together creates complex functionality.

3. **Automation Saves Time**: Creating reusable bash scripts for repetitive tasks like log analysis significantly improves efficiency. This script can be scheduled with cron for daily automated log monitoring and reporting.

---

`#90DaysOfDevOps` `#DevOpsKaJosh` `#TrainWithShubham`
