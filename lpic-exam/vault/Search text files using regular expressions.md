---
Weight: "3"
---
# Regular Expressions

The simplest regular expression contains at least one *atom*. An *atom*, is the basic element of a regular expression, it is just a character that may or may not have special meaning.

There are two types of Regular Expressions:
	- **Basic Regular Expressions (BRE)**
	- **Extended Regular Expressions (ERE)**

| RE                           | Purpose                                                              |
| ---------------------------- | -------------------------------------------------------------------- |
| **. (dot)**                  | Atom matches with any character                                      |
| **^ (caret)**                | Atom matches with the beginning of a line                            |
| **$ (dollar sign)**          | Atom matches with the end of a line                                  |
| **\[] (Bracket Expression)** | - Atom matches with a list of literal characters<br>- Accept classes |
- The `caret` and `dollar` sign atoms are used when only matches at the beginning or at the end of the string are of interest. For that reason they are also called *anchors*.
- The `^` is a literal character except when at the beginning and `$` is a literal character except when at the end of the regular expression.

| Bracket Class | Purpose                                                                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `[:alnum:]`   | Represents an alphanumeric character                                                                                                     |
| `[:alpha:]`   | Represents an alphabetic character                                                                                                       |
| `[:ascii:]`   | Represents a character that fits into the ASCII character set                                                                            |
| `[:blank:]`   | Represents a blank character, that is, a space or a tab                                                                                  |
| `[:cntrl:]`   | Represents a control character                                                                                                           |
| `[:digit:]`   | Represents a digit (0 through 9)                                                                                                         |
| `[:graph:]`   | Represents any printable character except space                                                                                          |
| `[:lower:]`   | Represents a lowercase character                                                                                                         |
| `[:print:]`   | Represents any printable character including space                                                                                       |
| `[:punct:]`   | Represents any printable character which is not a space or an alphanumeric character                                                     |
| `[:space:]`   | Represents white-space characters: space, form-feed (\f), newline (\n), carriage return (\r), horizontal tab (\t), and vertical tab (\v) |
| `[:upper:]`   | Represents an uppercase letter                                                                                                           |
| `[:xdigit:]`  | Represents hexadecimal digits (0 through F)                                                                                              |

# Quantifiers

Quantifiers are used to control how many times a pattern (Atom) can repeat.

**Common quantifiers**

| Quantifier | Meaning                       |
| ---------- | ----------------------------- |
| `*`        | 0 or more times               |
| `+`        | 1 or more times               |
| `?`        | 0 or 1 time                   |
| `{3}`      | exactly 3 times (Bound)       |
| `{2,5}`    | between 2 and 5 times (Bound) |

## Atom Sequences

When a quantifier is applied, regex looks for a **contiguous repetition** of the atom. A sequence is constructed by combining regex patterns (Atoms)

## Atom Piece

A **piece** is simply the part of the text that was matched (Atom) and it is the smallest individual building block of a regex pattern.

**Last sentence**
> Quantifiers control how many times a regex atom repeats, producing a contiguous matched sub-string called a piece, but the exact behavior can differ across regex standards and implementations.

# Branches and Back References

An extended regular expression can be divided into *branches*, each one an independent regular expression.

Branches are separated by `|` and the combined regular expression will match anything that corresponds to any of the branches.

BRE will interpret `|` as a literal character, but to allow branches use `\|`
BRE will interpret `(` and `)` as literal characters, but for subexpressions we use `\(` and `\)`

> [!Note]
> The backslash reference indicator is used like in extended regular expressions

# Searching with Regular Expressions

Regular expressions are extremely useful with `grep` and `find` because they let you search for files, text patterns, log entries, code fragments, and more.

## Common `grep` Uses

| Command                                                    | Purpose                             |
| ---------------------------------------------------------- | ----------------------------------- |
| `grep "^ERROR" logfile.txt`                                | Find lines beginning with a pattern |
| `grep "failed$" logfile.txt`                               | Find lines ending with a pattern    |
| `grep -E "[0-9]+" file.txt`                                | Find numbers                        |
| `grep -E "[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}"` | Match email addresses               |
| `grep "^$" file.txt`                                       | Find blank lines                    |
| `grep -E "^[0-9]+$" file.txt`                              | Find lines that contain only digits |

## Common `find` uses

| Command                | Purpose               |
| ---------------------- | --------------------- |
| `find . -name "*.txt"` | Find all `.txt` files |

## grep, egrep and fgrep

| Command | Meaning                | Regex Type                         | Special Characters Interpreted? |
| ------- | ---------------------- | ---------------------------------- | ------------------------------- |
| `grep`  | General pattern search | Basic Regular Expressions (BRE)    | Yes                             |
| `egrep` | Extended grep          | Extended Regular Expressions (ERE) | Yes                             |
| `fgrep` | Fixed-string grep      | No regex                           | No                              |

# The Stream Editor: sed

It reads text from standard input or from the files named on the command line, modifies this text and writes it to standard output.

**Sed Syntax**

```bash
s/old/new/option
```

| Options  | Purpose                |
| -------- | ---------------------- |
| `g`      | Replace all matches    |
| `d`      | Delete line            |
| `p`      | Print line             |
| `i\text` | Insert before line     |
| `a\text` | Append after line      |
| `c\text` | Replace line           |
| `-n`     | Suppress normal output |
| `-i`     | Edit file in place     |
| `-E`     | Use extended regex     |

**Common commands:**

| Command                                | Purpose                                                   |
| -------------------------------------- | --------------------------------------------------------- |
| `sed 's/error/warning/' logfile.txt`   | Replace first occurrence on each line                     |
| `sed 's/error/warning/g' logfile.txt`  | Replace all occurrences                                   |
| `sed -i 's/http:/https:/g' config.txt` | Edit a file in place                                      |
| `sed '5d' file.txt`                    | Delete line 5                                             |
| `sed '10,20d' file.txt`                | Delete lines 10 through 20                                |
| `sed '/^$/d' file.txt`                 | Delete blank lines                                        |
| `sed -n '5p' file.txt`                 | Prints only line 5                                        |
| `sed -n '10,20p' file.txt`             | Prints lines 10 through 20                                |
| `sed -n '/ERROR/p' logfile.txt`        | Print matching lines                                      |
| `sed '/START/i\New line inserted'`     | Insert before a line                                      |
| `sed '/START/a\Added after START'`     | Insert after a line                                       |
| `sed '/START/c\Logging disabled'`      | Replace lines matching a pattern                          |
| `sed 's/:.*//'`                        | Extract Columns or Fields                                 |
| `sed '/^#/d'`                          | Remove Comments                                           |
| `sed '=' file.txt`                     | Number lines                                              |
| `sed 's/^ *//'`                        | Removing leading spaces                                   |
| `sed 's/ *$//'`                        | Removing trailing spaces                                  |
| `sed 's/  */ /g'`                      | Removing leading spaces                                   |
| `sed 's/,/\t/g'`                       | Work with CSV-like Data (Replace `,` with horizontal tab) |
| `ls *.txt` \| `sed 's/.txt$/.bak/'`    | Rename files via Pipelines                                |
| `sed -n 's/.*\([0-9]\{4\}\).*/\1/p'`   | Extract Information Using Regex (Date)                    |


> [!Tip]
> In practice:
> - Use `grep` to find matching lines
> - Use `sed` to modify or transform text streams
> - Use `awk` when you need field-based processing, calculations, or reports

---