In Linux, **pipes** and **redirects** are tools for managing the input and output of commands, enabling efficient processing and manipulation of data.

---

## **1. Pipes (`|`)**

- **Description**:
    
    A pipe connects the standard output of one command to the standard input of another. It allows chaining commands.
    
- **Syntax**:
    
    ```bash
    command1 | command2
    
    ```
    
- **Example**:
    
    ```bash
    ls | grep "file"
    
    ```
    
    - The output of `ls` (list files) is sent to `grep` to filter lines containing "file".
- **Practical Uses**:
    - **Counting Lines**:
        
        ```bash
        cat file.txt | wc -l
        
        ```
        
        - Counts the number of lines in `file.txt`.
    - **Sorting and Displaying**:
        
        ```bash
        cat file.txt | sort | uniq
        
        ```
        
        - Sorts and removes duplicate lines from `file.txt`.

---

## **2. Redirection**

Redirection controls where a command reads its input or sends its output. It manipulates **stdin**, **stdout**, and **stderr**.

### **Input Redirection (`<`)**

- Redirects a file to standard input.
- **Syntax**:
    
    ```bash
    command < file
    
    ```
    
- **Example**:
    
    ```bash
    wc -l < file.txt
    
    ```
    
    - Counts the number of lines in `file.txt`.

---

### **Output Redirection (`>` and `>>`)**

- **`>`**: Redirects standard output to a file, overwriting its content.
- **`>>`**: Appends standard output to a file.
- **Syntax**:
    
    ```bash
    command > file
    command >> file
    
    ```
    
- **Example**:
    
    ```bash
    echo "Hello" > output.txt
    
    ```
    
    - Writes "Hello" to `output.txt`.
    
    ```bash
    echo "World" >> output.txt
    
    ```
    
    - Appends "World" to `output.txt`.

---

### **Error Redirection (`2>`, `2>>`)**

- Redirects standard error to a file.
- **Syntax**:
    
    ```bash
    command 2> error_file
    command 2>> error_file
    
    ```
    
- **Example**:
    
    ```bash
    ls nonexistentfile 2> error.log
    
    ```
    
    - Saves the error to `error.log`.

---

### **Combined Redirection (`>&`)**

- Combines stdout and stderr into the same stream.
- **Syntax**:
    
    ```bash
    command > file 2>&1
    
    ```
    
- **Example**:
    
    ```bash
    ls existingfile nonexistentfile > output.log 2>&1
    
    ```
    
    - Redirects both stdout and stderr to `output.log`.

---

### **Discarding Output (`/dev/null`)**

- Discards output by redirecting it to `/dev/null`.
- **Syntax**:
    
    ```bash
    command > /dev/null
    command 2> /dev/null
    command > /dev/null 2>&1
    
    ```
    
- **Example**:
    
    ```bash
    find / -name file 2> /dev/null
    
    ```
    
    - Searches for `file` and suppresses error messages.

---

### **Redirect stdin, stdout, and stderr Together**

- Redirecting all streams can be combined.
- **Syntax**:
    
    ```bash
    command < input_file > output_file 2> error_file
    
    ```
    
- **Example**:
    
    ```bash
    some_command < input.txt > output.txt 2> errors.log
    
    ```
    

---

## **Combining Pipes and Redirection**

- Pipes and redirection can be used together for complex tasks.
- **Example**:
    
    ```bash
    cat file.txt | grep "pattern" > filtered.txt
    
    ```
    
    - Filters lines containing "pattern" from `file.txt` and saves them to `filtered.txt`.
- **Another Example**:
    
    ```bash
    find / -name "*.txt" 2> errors.log | wc -l > count.txt
    
    ```
    
    - Finds all `.txt` files, counts them, and saves the count to `count.txt` while logging errors to `errors.log`.

---

## **Key Points**

| **Symbol** | **Purpose** | **Example** |
| --- | --- | --- |
| ` | ` | Pipe (connect stdout of one command to stdin of another) |
| `<` | Redirect stdin | `grep "pattern" < file.txt` |
| `>` | Redirect stdout (overwrite) | `echo "Hello" > file.txt` |
| `>>` | Redirect stdout (append) | `echo "World" >> file.txt` |
| `2>` | Redirect stderr (overwrite) | `command 2> error.log` |
| `2>>` | Redirect stderr (append) | `command 2>> error.log` |
| `>&` | Combine stdout and stderr | `command > file 2>&1` |
| `/dev/null` | Discard output | `command > /dev/null 2>&1` |

---
