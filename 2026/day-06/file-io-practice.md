# Day 06 – Linux Fundamentals: File Read & Write Practice

## 📌 Objective

Today’s goal was to practice basic file input/output operations using fundamental Linux commands.

This exercise focused on:

- Creating a file
- Writing content using redirection
- Appending new lines
- Reading full file content
- Reading partial content
- Writing and displaying content simultaneously

---

## 🛠 Commands I Practiced

### 1️⃣ Create a File
```bash
touch notes.txt
```
Creates an empty file named `notes.txt`.

---

### 2️⃣ Write Content Using `>`
```bash
echo "Linux file handling practice - Day 06" > notes.txt
```
Writes text into the file.  
⚠️ This overwrites existing content.

---

### 3️⃣ Append Content Using `>>`
```bash
echo "Redirection using > and >> operators" >> notes.txt
echo "Understanding file read and write operations" >> notes.txt
```
Appends new lines to the file without deleting existing content.

---

### 4️⃣ Write and Display Using `tee`
```bash
echo "Using tee to write and display output" | tee -a notes.txt
```
Writes to the file and displays output on terminal at the same time.

---

### 5️⃣ Read Full File Using `cat`
```bash
cat notes.txt
```
Displays complete file content.

---

### 6️⃣ Read First Few Lines Using `head`
```bash
head -n 2 notes.txt
```
Displays first 2 lines of the file.

---

### 7️⃣ Read Last Few Lines Using `tail`
```bash
tail -n 2 notes.txt
```
Displays last 2 lines of the file.

---

## 📂 Final File Content (notes.txt)

```
Linux file handling practice - Day 06
Redirection using > and >> operators
Understanding file read and write operations
Using tee to write and display output
```

---

## 🎯 What I Learned

- `>` overwrites file content.
- `>>` appends content safely.
- `tee` is useful for logging and scripting.
- `cat`, `head`, and `tail` are essential for log analysis.
- File handling is a daily DevOps activity (logs, configs, scripts).

---

## 🚀 Why This Matters in DevOps

In real-world DevOps:

- Logs are text files.
- Configuration files are text-based.
- Scripts generate output files.
- Monitoring tools store logs in files.

Being comfortable with file operations helps in:
- Troubleshooting issues
- Automating tasks
- Debugging production problems

---

## 🔥 Key Command I Will Use Often

`tail -f logfile.log`

This is extremely useful for real-time log monitoring in servers.

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
