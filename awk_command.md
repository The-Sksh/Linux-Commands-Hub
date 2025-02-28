The `awk` command is a powerful text processing tool in Linux and Unix-like systems. It is primarily used for pattern scanning, data extraction, and reporting. `awk` can process and manipulate data based on patterns and conditions, making it useful for tasks such as summarizing, calculating, or transforming data.

### **Basic Syntax of `awk`**:

```bash
awk 'pattern { action }' filename

```

- **pattern**: The condition that must be met for the action to execute (optional).
- **action**: The operation to be performed on matching lines (optional). If no action is specified, `awk` prints the entire line by default.
- **filename**: The file or input to process.

---

### **Common Features and Usage of `awk`**

1. **Print specific columns or fields**:
By default, `awk` treats text as fields separated by whitespace (spaces or tabs). You can specify which field you want to print using `$` followed by the field number.
    - **Print the first column**:
        
        ```bash
        awk '{print $1}' filename
        
        ```
        
        - This prints the first column of every line in the file.
    - **Print multiple columns**:
        
        ```bash
        awk '{print $1, $3}' filename
        
        ```
        
        - This prints the first and third columns of each line.
2. **Using a delimiter**:
You can specify a custom field delimiter using the `F` option.
    - **Set comma as a delimiter (CSV file)**:
        
        ```bash
        awk -F ',' '{print $1, $2}' filename.csv
        
        ```
        
        - This will print the first and second columns of a CSV file.
3. **Using patterns to match specific lines**:
You can specify a pattern to match only certain lines in a file. For example, you can print only lines containing a specific string.
    - **Print lines that contain the word "error"**:
        
        ```bash
        awk '/error/ {print $0}' filename
        
        ```
        
        - This prints the entire line (`$0` represents the whole line) only if it contains the string "error".
4. **Performing calculations**:
`awk` allows you to perform arithmetic operations on fields, such as summing numbers, averaging, etc.
    - **Sum the values of the second column**:
        
        ```bash
        awk '{sum += $2} END {print sum}' filename
        
        ```
        
        - This adds up all the values in the second column and prints the sum at the end.
    - **Average the values of the second column**:
        
        ```bash
        awk '{sum += $2; count++} END {print sum/count}' filename
        
        ```
        
        - This calculates the average of the numbers in the second column.
5. **Using `awk` with conditions**:
You can apply conditions to decide when an action should be performed.
    - **Print lines where the value in the second column is greater than 10**:
        
        ```bash
        awk '$2 > 10 {print $1, $2}' filename
        
        ```
        
        - This prints the first and second columns, but only for lines where the second column is greater than 10.
6. **Changing the output format**:
You can use `awk` to format the output in specific ways, such as printing with custom separators or adding text.
    - **Print the first and second columns separated by a dash**:
        
        ```bash
        awk '{print $1 "-" $2}' filename
        
        ```
        
        - This prints the first and second columns, separated by a dash.
    - **Formatted output with `printf`**:
        
        ```bash
        awk '{printf "Name: %-10s Age: %-3s\n", $1, $2}' filename
        
        ```
        
        - This prints the first column left-aligned to 10 characters and the second column left-aligned to 3 characters.
7. **Using built-in variables**:
`awk` provides several built-in variables to control its behavior and output.
    - **`NR`**: The number of records (lines) processed so far.
    - **`NF`**: The number of fields in the current record (line).
    - **`$0`**: The entire current line.
    - **`$1`, `$2`, ...**: The fields in the current record.
    - **Print the line number and the line**:
        
        ```bash
        awk '{print NR, $0}' filename
        
        ```
        
        - This prints the line number followed by the entire line.
    - **Print the number of fields in each line**:
        
        ```bash
        awk '{print NF}' filename
        
        ```
        
        - This prints the number of fields in each line of the file.
8. **Using `BEGIN` and `END` blocks**:
    - **`BEGIN` block**: Code in this block runs before processing any input lines.
    - **`END` block**: Code in this block runs after all input lines are processed.
    - **Example: Print a header and sum up values**:
        
        ```bash
        awk 'BEGIN {print "Name\tAge"} {sum += $2} END {print "Total Sum: ", sum}' filename
        
        ```
        
        - This prints a header before processing lines and prints the sum at the end.

---

### **Examples of `awk` Commands**

1. **Print specific columns**:
    
    ```bash
    awk '{print $1, $3}' data.txt
    
    ```
    
    - This prints the first and third columns of each line in `data.txt`.
2. **Print lines where the second column is greater than 50**:
    
    ```bash
    awk '$2 > 50' data.txt
    
    ```
    
3. **Sum the values in the second column**:
    
    ```bash
    awk '{sum += $2} END {print sum}' data.txt
    
    ```
    
4. **Calculate the average of the second column**:
    
    ```bash
    awk '{sum += $2; count++} END {print sum/count}' data.txt
    
    ```
    
5. **Print only the lines containing the string "Error"**:
    
    ```bash
    awk '/Error/' logfile.txt
    
    ```
    
6. **Print the line number and content**:
    
    ```bash
    awk '{print NR, $0}' data.txt
    
    ```
    
7. **Using custom field delimiter**:
    
    ```bash
    awk -F ',' '{print $1, $2}' data.csv
    
    ```
    
    - This specifies a comma as the delimiter for fields in a CSV file.
8. **Print the first 10 characters of each line**:
    
    ```bash
    awk '{print substr($0, 1, 10)}' data.txt
    
    ```
    

---

### **Summary of Key `awk` Features**

| **Feature** | **Description** | **Example** |
| --- | --- | --- |
| **Print specific field** | Print a specific field in a line | `awk '{print $1}' file.txt` |
| **Field delimiter** | Specify a delimiter for fields | `awk -F ',' '{print $1}' file.csv` |
| **Conditions** | Perform actions based on conditions | `awk '$2 > 10 {print $1, $2}' file.txt` |
| **Calculations** | Perform arithmetic operations | `awk '{sum += $2} END {print sum}' file.txt` |
| **Formatted output** | Format the output using `printf` | `awk '{printf "%-10s %-5s\n", $1, $2}' file.txt` |
| **Built-in variables** | Use built-in variables like `NR`, `NF`, `$0`, `$1`, etc. | `awk '{print NR, $0}' file.txt` |
| **BEGIN/END blocks** | Code that runs before or after processing the file | `awk 'BEGIN {print "Header"} {print $1} END {print "Done"}' file.txt` |

The `awk` command is extremely versatile for text processing and is widely used for tasks such as reporting, data extraction, and calculations within text files.
