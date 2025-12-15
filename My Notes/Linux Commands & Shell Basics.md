# Linux Commands & Shell Basics

## 1. File & Directory Operations

### Copy, Create, Delete

```bash
cp -R source destination      # Recursively copy directories and files
mkdir -p path/to/dir          # Recursively create directory structure
rm -r directory               # Recursively delete directory
rm -rf directory              # Recursively and forcefully delete (no prompt)
```

---

## 2. File Permissions

### Symbolic Permission Changes

```bash
chmod u+w,g+w,o+w a.txt        # Add write permission to user, group, others
```

Example output:

```text
-rw-rw-rw-. 1 smartool smartool 21 Dec 14 09:07 a.txt
```

### Reset Permissions to Read-Only

```bash
chmod a=r a.txt               # Reset permissions to read-only for all
```

Example output:

```text
-r--r--r--. 1 smartool smartool 21 Dec 14 09:07 a.txt
```

### Recursive Permission Change

```bash
chmod -R 777 nishith/          # Recursively apply full permissions
```

Directory listing:

```text
drwxrwxrwx. 2 smartool smartool 32 Dec 14 09:11 nishith
```

Contents:

```bash
ls -ltr nishith/
```

```text
-rwxrwxrwx. 1 smartool smartool 21 Dec 14 09:07 a.txt
-rwxrwxrwx. 1 smartool smartool  0 Dec 14 09:11 b.txt
```

---

## 3. File Globbing (Wildcards)

```bash
ls -ltr my*                   # Files starting with 'my'
ls -ltr *.???                 # Files with 3-character extensions
ls -ltr *.{zip,pdf}           # Files ending with .zip or .pdf
ls -ltr *.(txt|pdf)           # Files ending with txt or pdf (shell dependent)
ls -ltr (f|m)*                # Files starting with f or m (tcsh syntax)
ls -ltr [fm]*                 # Files starting with f or m
ls -ld [A-Z]*                 # Files/directories starting with uppercase letters
ls -ld [[:upper:]]*           # Same as above (not supported in tcsh)
```

---

## 4. Symbolic Links

```bash
sudo ln -s /home/smartool/nishith/bin/myscript.sh /bin
```

It creates a symbolic link in `/bin` so that `myscript.sh` can be run from anywhere like a normal system command.
The `ln` Stands for link and is used to create links between files
`-s` Creates a symbolic (soft) link. Not a copy and points to the original file.

**Verification:**
```bash
ls -ltr /bin/my*
```
![4da94ebda0b5705788aaec7613356d21.png](../_resources/4da94ebda0b5705788aaec7613356d21.png)

---

## 5. Searching Manual Pages

### Build Man Page Index

```bash
sudo mandb                    # Build manual page index
```

### Search Commands

```bash
apropos zip                   # Search commands related to 'zip'
man -k search                 # Same as apropos
man -k -s 1 password          # Section 1 commands related to 'password'
```


The `apropos` searches the Linux manual (man) pages and shows commands related to a keyword.
**For example:**
![769960c902609fd8d666667d01928a9d.png](../_resources/769960c902609fd8d666667d01928a9d.png)

![60ecc741d40d8994c06a92d82816d093.png](../_resources/60ecc741d40d8994c06a92d82816d093.png)

![680a06a2953693484b19367d4569c900.png](../_resources/680a06a2953693484b19367d4569c900.png)

---

## 6. Viewing Files

```bash
cat -n file_name               # Display file with line numbers
```

---

## 7. Disk & File Storage

### Disk Free (Filesystem Level)

```bash
df -h                          # Human-readable disk free space
```

![4781bf3339e7957df4916de28bd6fde0.png](../_resources/4781bf3339e7957df4916de28bd6fde0.png)

### Disk Usage (Directory/File Level)

```bash
du -ah                         # Displays disk usage at the file and directory level.
```

Sample output:

![4fa06ac69c694ce320193f32af9781d3.png](../_resources/4fa06ac69c694ce320193f32af9781d3.png)

**`du -ah` vs `df -h`**
| Command  | Tells you                  |
| -------- | -------------------------- |
| `df -h`  | Filesystem free space      |
| `du -ah` | File/directory space usage |


---

## 8. Keyboard Shortcuts (Shell Editing)

```text
Ctrl + f   → Move cursor one character forward
Ctrl + b   → Move cursor one character backward
Alt  + f   → Move cursor one word forward
Alt  + b   → Move cursor one word backward
Ctrl + a   → Move to beginning of the line
Ctrl + e   → Move to end of the line
Ctrl + d   → Delete one character to the right
Ctrl + w   → Delete all text to the left
```

---

## 9. Variables (tcsh)

### Shell Variables

```bash
set msg="Hello World"
echo "$msg"
```

Output:

```text
Hello World
```

### List and Search Variables

```bash
set | less                   # List all tcsh variables
set | grep msg               # Search for a variable
```

### Environment Variables

```bash
setenv msg "Hello World"    # Export variable (similar to bash export)
/bin/tcsh                    # Start a new tcsh shell
echo $msg                    # Accessible due to setenv
```

### Unset Variables

```bash
unset msg                    # Remove shell variable
unsetenv msg                 # Remove environment variable
```

### Source Profile

```bash
source filename              # Reload a profile or script
```

---

## 10. Job Control

### Job Types

* **Foreground jobs** – running and taking input
* **Background jobs** – running without terminal interaction

![7fbfd59551d28a6932a0acec72cc8f55.png](../_resources/7fbfd59551d28a6932a0acec72cc8f55.png)

### Commands

```text
Ctrl + Z   → Pause a running job
jobs       → List active jobs
fg 1       → Bring job 1 to foreground
Ctrl + C   → Terminate a running program
command &  → Run command in background
watch cmd  → Run a command repeatedly
```

---

## 11. Jobs vs Processes

| Concept | Managed By | Identifier     |
| ------- | ---------- | -------------- |
| Job     | Shell      | Job ID (1,2,3) |
| Process | Kernel     | PID            |

Example:

```bash
watch date &
```

Output:

```text
[3] 1457262
```

* **3** → Job ID
* **1457262** → Process ID (PID)

---

## 12. Process Management

```bash
ps                            # View processes in current terminal
```

Important columns:

* **PID** – Process ID
* **TTY** – Terminal (TeliType)
* **CMD** – Command name

![e79a1b715fd2e40215f31c4663c82144.png](../_resources/e79a1b715fd2e40215f31c4663c82144.png)

---

## 13. Signals & Killing Processes
```bash
kill -l                       # List all signals
```

![f9a6d92b62a5b64d763e5b328d8179c2.png](../_resources/f9a6d92b62a5b64d763e5b328d8179c2.png)

```bash
kill -9 PID                   # Force kill a process
```

![677f773d6041e3b353175cb2fbb4a00f.png](../_resources/677f773d6041e3b353175cb2fbb4a00f.png)

---

## 14. Redirection and Piping

### Standard Streams in Unix
Every Unix command works with three default streams:

| Stream | Name            | Description                    | Default Destination |
| ------ | --------------- | ------------------------------ | ------------------- |
| STDIN  | Standard Input  | Where command reads input from | Keyboard            |
| STDOUT | Standard Output | Normal command output          | Terminal (screen)   |
| STDERR | Standard Error  | Error messages                 | Terminal            |

By default:

* Output → **STDOUT → terminal**

#### Output Redirection (`>`)
```bash
echo "Hello World" > sample.txt
```

What happens:

* `echo` sends output to **STDOUT**
* `>` redirects STDOUT into `sample.txt`
* File is **created if it does not exist**
* File is **overwritten if it exists**

#### Overwriting vs Appending
**Overwrite (`>`)**
```bash
echo "Another try" > sample.txt
```
* Existing content is **discarded**
* File is rewritten from scratch

**Append (`>>`)**
```bash
echo "Hello World" >> sample.txt
```
* New content is added to the **end of the file**
* Existing content is preserved

Result:

```text
Another try
Hello World
```

### Piping (`|`)
A pipe sends:

```
STDOUT of command A → STDIN of command B
```

**Example:**
```bash
ls -l | grep Sam | awk '{print $9}'
```

1. `ls -l`             : Produces detailed file listing
2. `grep Sam`       : Keeps only lines containing `Sam`
3. `awk '{print $9}'`:  Extracts the **9th field** (filename)

![4baa6550df7029ddf4e10d49e3bcc7e4.png](../_resources/4baa6550df7029ddf4e10d49e3bcc7e4.png)

---

### Redirecting Errors (STDERR) and `/dev/null` 
Some commands (like `find`) produce a lot of **error messages** (for example: `Permission denied`).

![cbc78b78f4dc9d70025a663f66704e4a.png](../_resources/cbc78b78f4dc9d70025a663f66704e4a.png)

These messages are often just **noise** when you're only interested in the actual results.

**STDOUT vs STDERR**
Unix commands typically use two output streams:

* **STDOUT (1)**: normal results/output
* **STDERR (2)**: error messages
Even if both appear on the screen by default, they are **different streams**.

**File descriptor numbers**

| Stream | Name            | Descriptor |
| ------ | --------------- | ---------- |
| STDIN  | standard input  | `0`        |
| STDOUT | standard output | `1`        |
| STDERR | standard error  | `2`        |

**Redirecting only STDOUT does NOT capture errors**
If you run:

```bash
find / -name junk > results.txt
```

You might still see many errors on screen.

![39068885716b4d720f88cd1eab7b0b3d.png](../_resources/39068885716b4d720f88cd1eab7b0b3d.png)

Why?

* `>` redirects **STDOUT (1)** only
* Errors are sent to **STDERR (2)**

So `results.txt` can be empty even though the screen shows lots of errors.

#### Redirect STDERR to a file (`2>`)
To capture errors:

```bash
find / -name junk 2> errors.txt
```
**Effect:**
* Error messages no longer print on the screen
* They are saved into `errors.txt`

**View the captured errors:**

![2977dc2d0d3261e492fed2c67dc6d14e.png](../_resources/2977dc2d0d3261e492fed2c67dc6d14e.png)

#### Suppress STDERR using `/dev/null`
If you do not care about error messages at all:
```bash
find / -name junk 2> /dev/null
```
**Explanation:**

![b0d552cbb15aa850fd9d83d338c7a6d0.png](../_resources/b0d552cbb15aa850fd9d83d338c7a6d0.png)

* Results are displayed to `STDOUT`. Errors to `/dev/null`
* `/dev/null` is a special “null” file
* Anything written to it is discarded immediately
* This is commonly used to **hide unwanted output**

**Redirect BOTH: STDERR to `/dev/null` and STDOUT to a file**
```bash
find ./ -name errors.txt 2> /dev/null > output.txt
```
**What happens:**
* `2> /dev/null` → suppresses **errors**
* `> output.txt` → saves normal output (matches) into a file


## 15. VIM
- `vi` is a classic Unix text editor that is installed on almost every Unix/Linux system.
- `vim` stands for **“Vi IMproved”** (a newer, enhanced replacement for `vi`).
- On many modern systems, running `vi` actually launches `vim`.

![525ebfd2e1734127cf7b259f397d7c82.png](../_resources/525ebfd2e1734127cf7b259f397d7c82.png)

  **Modes in Vim**
* **Command mode**: navigate, run commands (default when you open a file)
* **Insert mode**: type/edit text

**Switch modes**
| Action                 | Key   |
| ---------------------- | ----- |
| Enter insert mode      | `i`   |
| Return to command mode | `Esc` |

### Navigation in command mode
**Move one character / line**
| Direction | Key |
| --------- | --- |
| Left      | `h` |
| Right     | `l` |
| Down      | `j` |
| Up        | `k` |

Arrow keys often work, but `h/j/k/l` keeps hands on home row.

**Page movement**
| Action    | Key                |
| --------- | ------------------ |
| Page down | `Ctrl+f` (forward) |
| Page up   | `Ctrl+b` (back)    |

**Jump to beginning/end of a line**
| Action        | Key |
| ------------- | --- |
| Start of line | `0` |
| End of line   | `$` |

**Jump to beginning/end of the file**
Press `:` to enter command-line mode inside vim.
| Action              | Command      |
| ------------------- | ------------ |
| Go to start of file | `:0` + Enter |
| Go to end of file   | `:$` + Enter |

**Basic word movement**
| Key | What it does                         |
| --- | ------------------------------------ |
| `w` | Move to **start of next word**       |
| `b` | Move to **start of previous word**   |
| `e` | Move to **end of current/next word** |


### Insert vs Append
Insert at cursor: `i`
Append after cursor: `a`
Append at end of line: `Shift+a`
Insert at beginning of line: `Shift+i`

### Deleting text
Delete a full line: `dd`
Delete a character under the cursor:`x`
Undo: `u`

### Repeat commands with a number prefix
You can run many vim commands multiple times by prefixing a number:
Delete 4 lines: `4dd`
Delete 25 characters: `25x`

### Searching within the file
Search forward: `/keyword`
Search backward: `?keyword`
Press **Enter** to jump to the match.

### Global search and replace
Enter command-line mode with `:` and use substitute.
Replace everywhere in the file:
```vim
:%s/import/export/
```
* `:%` = entire file
* `s` = substitute

`Vim` supports full regular expressions in substitutions.

### Saving and quitting
| Action                      | Command |
| --------------------------- | ------- |
| Save (write)                | `:w`    |
| Quit                        | `:q`    |
| Save and quit               | `:wq`   |
| Quit without saving (force) | `:q!`   |

**Save to a new file (copy)**
```vim
:w OtherFile.java
```

### Basic Copy & Paste
| Action            | Command | What it does                           |
| ----------------- | ------- | -------------------------------------- |
| Copy current line | `yy`    | Copies (yanks) the entire line         |
| Copy N lines      | `5yy`   | Copies 5 lines starting from cursor    |
| Paste below       | `p`     | Pastes copied content **below** cursor |
| Paste above       | `P`     | Pastes copied content **above** cursor |
| Cut (delete) line | `dd`    | Deletes line and copies it             |
| Cut N lines       | `5dd`   | Deletes 5 lines and copies them        |
| Undo              | `u`     | Undo last action                       |


## 16. Text Commands

### `head` and `tail` Commands
The `head` and `tail` commands are used to quickly view parts of large text files without opening the entire file.

`head filename`: Displays the first 10 lines of a file by default.
`tail filename`: Displays the last 10 lines of a file by default.
`head -n 3 filename.csv`: Shows the first 3 lines.
`tail -n 5 people-list.csv`: Shows the last 5 lines.

`tail -f logfile.log`: 
		- Displays the last lines of a file
		- Continues running
		- Shows new lines as they are appended

### `wc` Command
The `wc` command stands for **Word Count**.
The `wc` command counts:
- Lines (technically: newline characters)
- Words
- Bytes / characters
- `wc` prints newline, word, and byte counts for each file.
It works on **files** or on **input** received from another command via **piping**.

![91999b9be1696b9c151c2fb0f135a6ba.png](../_resources/91999b9be1696b9c151c2fb0f135a6ba.png)

**Common options**

| Option | Meaning                    |
| ------ | -------------------------- |
| `-l`   | Count lines only           |
| `-w`   | Count words only           |
| `-c`   | Count bytes                |
| `-m`   | Count characters           |
| `-L`   | Length of the longest line |

**Validate output size from another command**

```bash
ls -ltr | wc -l
```

### The `sort` Command
It is used to **sort lines of text**.
```bash
sort fruits.txt
```

![85aa803e5ac05da008739fbf2788ec4e.png](../_resources/85aa803e5ac05da008739fbf2788ec4e.png)

**Sorting via pipes**
```bash
cat fruits.txt | sort
```

![fe98897a7e7f2f7b90e498436a91620b.png](../_resources/fe98897a7e7f2f7b90e498436a91620b.png)

**Numeric sorting problem**

![e10967fb5fdd30f570848d739c1d3cf8.png](../_resources/e10967fb5fdd30f570848d739c1d3cf8.png)

**Numeric sort**
To sort numerically, use `-g` option.
```bash
sort -g numbers.txt
```

![b431a2b1e22e2c8f891b46e568d1711f.png](../_resources/b431a2b1e22e2c8f891b46e568d1711f.png)

**Reverse sorting** 

```bash
sort -g -r numbers.txt
```

**Other useful sort options**

| Option | Meaning                           |
| ------ | --------------------------------- |
| `-g`   | General numeric sort              |
| `-n`   | Numeric sort                      |
| `-r`   | Reverse order                     |
| `-M`   | Sort by month names (Jan, Feb, …) |
| `-h`   | Human-readable numbers (K, M, G)  |
| `-R`   | Random sort                       |

**Sorting by column**
* **Field** = column
* CSV fields are separated by commas
* `sort` supports column-based sorting

| Option | Meaning                  |
| ------ | ------------------------ |
| `-t`   | Field delimiter          |
| `-k`   | Sort key (column number) |

```bash
head -n 5 people_list.csv | tail -n +2 | sort -t '/' -k 3
```

![1ac66264c3b9ec8d4b68b2fedb7133a4.png](../_resources/1ac66264c3b9ec8d4b68b2fedb7133a4.png)
