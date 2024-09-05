

<h1 align="center"> Useful Command</h1>

# 1. `grep`

The `grep` command is a powerful tool in Unix/Linux used for searching text or patterns within files. The name "grep" stands for "Global Regular Expression Print," and it is widely used to search for specific strings or patterns in a file or output.

## Basic Usage

The basic syntax of the `grep` command is:

```bash
grep [options] pattern [file...]
```

- **`pattern`**: The text or regular expression you want to search for.
- **`file`**: The file or files in which you want to search for the pattern.

## Common Options

- **`-i`**: Ignore case (case-insensitive search).
- **`-r` or `-R`**: Recursively search directories.
- **`-v`**: Invert match (show lines that do **not** match the pattern).
- **`-n`**: Display line numbers along with the matching lines.
- **`-c`**: Count the number of matches.
- **`-l`**: List filenames containing the pattern.
- **`-e`**: Allows you to specify multiple patterns to search.
- **`-o`**: Show only the matched parts of the line.

## Examples

### 1. Search for a word in a file

```bash
grep "apple" file.txt
```

This command searches for the word "apple" in `file.txt` and displays the lines containing it.

### 2. Case-insensitive search

```bash
grep -i "apple" file.txt
```

This will find "apple", "Apple", "APPLE", etc., in `file.txt`.

### 3. Search recursively in directories

```bash
grep -r "apple" /path/to/directory
```

This command searches for "apple" in all files within the specified directory and its subdirectories.

### 4. Count occurrences of a word

```bash
grep -c "apple" file.txt
```

This will return the number of lines that contain the word "apple" in `file.txt`.

### 5. Show line numbers

```bash
grep -n "apple" file.txt
```

This displays matching lines with their line numbers in `file.txt`.

### 6. List files with matching pattern

```bash
grep -l "apple" *.txt
```

This lists all `.txt` files in the current directory that contain the word "apple".

### 7. Invert match (exclude lines with the pattern)

```bash
grep -v "apple" file.txt
```

This shows all lines in `file.txt` that do **not** contain the word "apple".

### 8. Multiple patterns

```bash
grep -e "apple" -e "orange" file.txt
```

This searches for lines containing either "apple" or "orange" in `file.txt`.

### 9. Show only the matched text

```bash
grep -o "apple" file.txt
```

This displays only the matched parts of the lines, in this case, just "apple".

## Advanced Example

Suppose you have a log file and you want to find all occurrences of the word "error", ignoring case, and also see the line numbers where these occurrences happen:

```bash
grep -i -n "error" /var/log/syslog
```

This command searches the `syslog` file for "error" (regardless of case) and shows you each matching line along with its line number.

## Combining with Other Commands

`grep` can be used in combination with other commands using pipes (`|`):

```bash
ps aux | grep "apache"
```

This searches the list of running processes for "apache".

## Conclusion

`grep` is a versatile and essential tool in any Unix/Linux user's toolkit. Whether you're searching through configuration files, logs, or even just text files, `grep` provides a quick and efficient way to find what you're looking for.
```

This format should look good on GitHub with the proper markdown syntax for code blocks and headings.
