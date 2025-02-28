Wildcards in Linux are special characters used in command-line operations to represent patterns, making it easier to select multiple files or directories at once. Here's a breakdown of common wildcards and their usage:

---

### **Types of Wildcards**

| Wildcard | Description | Example Usage | Explanation |
| --- | --- | --- | --- |
| `*` | Matches **zero or more characters**. | `ls *.txt` | Lists all files ending with `.txt`. |
| `?` | Matches **exactly one character**. | `ls file?.txt` | Matches `file1.txt`, `fileA.txt`, etc. |
| `[ ]` | Matches **any one character inside the brackets**. | `ls file[123].txt` | Matches `file1.txt`, `file2.txt`, `file3.txt`. |
| `[! ]` | Matches **any character not inside the brackets**. | `ls file[!1].txt` | Matches files like `file2.txt` but not `file1.txt`. |
| `{ }` | Matches **exact patterns separated by commas**. | `ls {file1,file2}.txt` | Matches `file1.txt` and `file2.txt`. |
| `\` | Escapes a wildcard to treat it as a literal character. | `ls file\*.txt` | Matches a file literally named `file*.txt`. |

---

### **Examples of Wildcards in Commands**

### **1. Using `` to Match Multiple Files**

```bash
ls *.log

```

- Matches all files ending in `.log`.

```bash
cp * /backup/

```

- Copies all files in the current directory to `/backup/`.

---

### **2. Using `?` to Match Single Characters**

```bash
ls file?.txt

```

- Matches files like `file1.txt` and `fileA.txt`.

---

### **3. Using `[ ]` to Match Specific Characters**

```bash
ls file[abc].txt

```

- Matches `filea.txt`, `fileb.txt`, and `filec.txt`.

---

### **4. Using `[! ]` to Exclude Characters**

```bash
ls file[!a-z].txt

```

- Matches files where the character in the brackets is not a lowercase letter.

---

### **5. Using `{ }` for Specific Patterns**

```bash
ls {file1,file2}.txt

```

- Matches exactly `file1.txt` and `file2.txt`.

```bash
mv {file1,file2}.txt /data/

```

- Moves `file1.txt` and `file2.txt` to `/data/`.

---

### **6. Escaping Wildcards with `\`**

```bash
ls file\*.txt

```

- Looks for a file literally named `file*.txt`, not files matching the `` wildcard.

---

### **Practical Use Cases**

1. **Cleaning Up Files**:
    
    ```bash
    rm *.tmp
    
    ```
    
    - Deletes all temporary files with `.tmp` extension.
2. **Batch Renaming**:
    
    ```bash
    mv file[1-3].txt archive/
    
    ```
    
    - Moves `file1.txt`, `file2.txt`, and `file3.txt` to `archive/`.
3. **Copying Selected Files**:
    
    ```bash
    cp file{A,B,C}.log /logs/
    
    ```
    
    - Copies `fileA.log`, `fileB.log`, and `fileC.log` to `/logs/`.

---

### **Combining Wildcards**

Wildcards can also be combined for complex patterns:

```bash
ls *[0-9]?.{txt,log}

```

- Matches files that:
    - End with a single digit followed by one other character.
    - Have `.txt` or `.log` extensions.

---

### **Note**

Wildcards are commonly used with commands like `ls`, `cp`, `mv`, `rm`, `find`, etc. Be cautious when using them with destructive commands like `rm` to avoid accidental deletions.
