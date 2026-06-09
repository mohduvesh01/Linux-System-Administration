# Input and Output (I/O) Redirection in Linux

## Introduction

In Linux, every program communicates using streams of data called Input and Output (I/O).

I/O Redirection allows users to control where input comes from and where output goes.

Instead of displaying output on the screen, Linux can:

* Save output to files
* Read input from files
* Redirect errors to files
* Pass output from one command to another

I/O Redirection is widely used in:

* Linux Administration
* Shell Scripting
* Automation
* DevOps
* Log Management

---

# Understanding Standard Streams

Every Linux process has three standard streams.

| Stream          | Number | Description    |
| --------------- | ------ | -------------- |
| Standard Input  | 0      | Input source   |
| Standard Output | 1      | Normal output  |
| Standard Error  | 2      | Error messages |

---

## Standard Input (stdin)

Default input source:

```text
Keyboard
```

Example:

```bash
cat
```

User enters:

```text
Linux
```

Output:

```text
Linux
```

---

## Standard Output (stdout)

Default output destination:

```text
Terminal Screen
```

Example:

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

---

## Standard Error (stderr)

Used for displaying errors.

Example:

```bash
ls wrongdirectory
```

Output:

```text
ls: cannot access 'wrongdirectory'
```

---

# Linux I/O Flow

```text
Keyboard
    │
    ▼
 Standard Input (0)
    │
    ▼
  Program
    │
 ┌──┴──┐
 ▼     ▼
Output Error
(1)   (2)
 │     │
 ▼     ▼
Screen Screen
```

---

# Output Redirection (>)

The `>` operator redirects output to a file.

Syntax:

```bash
command > file
```

---

## Example

```bash
ls > files.txt
```

Instead of displaying files on the screen:

```text
files.txt
```

contains:

```text
Documents
Downloads
Pictures
```

---

## Important Note

If the file already exists:

```bash
ls > files.txt
```

overwrites its contents.

---

# Append Output (>>)

The `>>` operator appends output to an existing file.

Syntax:

```bash
command >> file
```

---

## Example

```bash
echo "Linux" >> notes.txt
```

Existing file:

```text
Python
```

After command:

```text
Python
Linux
```

---

# Difference Between > and >>

| Operator | Action    |
| -------- | --------- |
| >        | Overwrite |
| >>       | Append    |

Interview Favorite ⭐

---

# Input Redirection (<)

The `<` operator takes input from a file.

Syntax:

```bash
command < file
```

---

## Example

Create file:

```text
input.txt
```

Content:

```text
Linux Administration
```

Command:

```bash
cat < input.txt
```

Output:

```text
Linux Administration
```

---

# Error Redirection (2>)

Redirects error messages to a file.

Syntax:

```bash
command 2> error.txt
```

---

## Example

```bash
ls wrongdirectory 2> error.txt
```

Screen:

```text
No error displayed
```

File:

```text
error.txt
```

contains:

```text
ls: cannot access 'wrongdirectory'
```

---

# Append Error Output (2>>)

Adds errors to an existing file.

```bash
ls wrongdirectory 2>> errors.log
```

---

# Redirect Standard Output and Error

Save both output and errors.

```bash
command > output.txt 2> error.txt
```

Example:

```bash
ls /home > output.txt 2> error.txt
```

---

# Redirect Everything to One File

```bash
command > result.txt 2>&1
```

Meaning:

```text
stdout → result.txt
stderr → result.txt
```

Example:

```bash
ls /home wrongdirectory > result.txt 2>&1
```

---

# Discard Output Using /dev/null

Linux provides a special file:

```text
/dev/null
```

Anything sent there is discarded.

Example:

```bash
ls > /dev/null
```

Output is ignored.

---

## Ignore Errors

```bash
ls wrongdirectory 2> /dev/null
```

Error messages disappear.

---

# Pipes (|)

A pipe sends the output of one command directly to another command.

Syntax:

```bash
command1 | command2
```

---

## Example

```bash
ls | grep ".txt"
```

Workflow:

```text
ls
 │
 ▼
List Files
 │
 ▼
grep ".txt"
 │
 ▼
Show Only TXT Files
```

Output:

```text
notes.txt
report.txt
```

---

## Another Example

```bash
cat users.txt | grep "admin"
```

Displays only lines containing:

```text
admin
```

---

# Combining Multiple Commands

Example:

```bash
cat logfile.txt | grep "error" > errors.txt
```

Workflow:

```text
Read Log File
      │
      ▼
Search "error"
      │
      ▼
Save Results
```

---

# Practical Examples

## Save Directory Listing

```bash
ls -l > files.txt
```

---

## Append New Entry

```bash
echo "Backup Completed" >> backup.log
```

---

## Redirect Errors

```bash
find /root 2> errors.log
```

---

## Search and Save Results

```bash
grep "failed" auth.log > failed_logins.txt
```

---

## Count Users

```bash
cat users.txt | wc -l
```

Output:

```text
25
```

---

# Real-Life Scenario

A system administrator wants to find login failures.

Command:

```bash
grep "Failed" /var/log/auth.log > failed_logins.txt
```

Result:

```text
All failed login attempts are stored in a file.
```

This can later be reviewed or shared.

---

# Commonly Used Redirection Operators

| Operator | Purpose                        |
| -------- | ------------------------------ |
| >        | Redirect output                |
| >>       | Append output                  |
| <        | Redirect input                 |
| 2>       | Redirect errors                |
| 2>>      | Append errors                  |
| 2>&1     | Redirect stdout and stderr     |
| |        | Pipe output to another command |

---

# Interview Questions

## Basic

1. What is I/O Redirection?
2. What is stdin?
3. What is stdout?
4. What is stderr?

---

## Intermediate

5. Difference between > and >>?
6. What is a pipe?
7. What does 2> mean?
8. What is /dev/null?

---

## Advanced

9. Explain 2>&1.
10. How would you redirect errors to a file?
11. How would you save both output and errors in one file?
12. Explain the flow of data through pipes.

---

# Viva Questions

### Q: Difference between > and >>?

**Answer:**

`>` overwrites an existing file, while `>>` appends new content to the end of the file.

---

### Q: What is a pipe in Linux?

**Answer:**

A pipe (`|`) passes the output of one command as the input to another command, allowing commands to work together.

---

### Q: What is /dev/null?

**Answer:**

`/dev/null` is a special file that discards all data written to it. It is commonly used to suppress unwanted output or error messages.

---

### Q: Explain 2>&1.

**Answer:**

`2>&1` redirects standard error (2) to the same location as standard output (1), allowing both outputs to be stored in the same file.

---

# Summary

I/O Redirection is a fundamental Linux concept that allows users to control input, output, and error streams. Operators such as `>`, `>>`, `<`, `2>`, and `|` enable efficient data handling, automation, log management, and shell scripting. Mastering I/O Redirection is essential for Linux Administration, DevOps, and System Engineering roles.
