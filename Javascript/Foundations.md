# Foundations

## Workspace/Session

---

- `//` inserts a one-line comment
- `/* … */` inserts a multi-line comment
- `alert()` outputs data in an alert box in the browser window
- `confirm()` opens a yes/no dialog and returns true/false depending on user input
- `console.log()` writes information to the browser console; good for debugging purposes
- `document.write()` writes directly to the HTML document
- `prompt()` creates dialogue box to capture user input

## Operators

---

### Basic Operators

| **Operator** | **Description** |
| --- | --- |
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `()` | Grouping; operations within parentheses are executed first (PEMDAS) |
| `%` | Modulus division |
| `++` | Increment operator |
| `--` | Decrement operator |
| `+=` | Compounding operator |

### Comparison Operators

| **Operator** | **Description** |
| --- | --- |
| `==` | Equal to |
| `===` | Equal value and equal data type |
| `!=` | Not equal to |
| `!==` | Not equal value or not equal type |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |
| `?` | Ternary operator |

### Logical Operators

| **Operator** | **Description** |
| --- | --- |
| `&&` | 'AND' operator |
| `||` | 'OR' operator |
| `!` | 'NOT' operator |

### Bitwise Operators

| **Operator** | **Description** |
| --- | --- |
| `&` | 'AND' statement |
| `|` | 'OR' statement |
| `~` | 'NOT' |
| `^` | 'XOR' |
| `<<` | Left shift |
| `>>` | Right shift |
| `>>>` | Zero fill right shift |

## Regular Expression Syntax

---

### Pattern Modifiers

| **Modifier** | **Description** |
| --- | --- |
| `e` | Evaluate replacement |
| `i` | Perform case-insensitive matching |
| `g` | Perform global matching |
| `m` | Perform multiple line matching |
| `s` | Treat strings as single line |
| `x` | Allow comments and whitespace in patter |
| `U` | Ungreedy pattern |

### Brackets

| **Modifier** | **Description** |
| --- | --- |
| `[abc]` | Find any of the characters between the brackets |
| `[^abc]` | Find any character not in the brackets |
| `[0-9]` | Used to find any digit from 0 to 9 |
| `[A-z]` | Find any character from uppercase A to lowercase z |
| `(a\|b\|c)` | Find any of the alternatives separated with "\|" |

### Metacharacters

| **Modifier** | **Description** |
| --- | --- |
| `.` | Find a single character, except a new line or a line terminator |
| `\w` | Word character |
| `\W` | Non-word character |
| `\d` | A digit |
| `\D` | A non-digit character |
| `\s` | Whitespace character |
| `\S` | Non-whitespace character |
| `\b` | Find a match at the beginning or end of a word |
| `\B` | A match not at the beginning or end of a word |
| `\0` | NUL character |
| `\f` | Form feed character |
| `\r` | Carriage return character |
| `\t` | Tab character |
| `\v` | Vertical tab character |
| `\xxx` | The character specified by an octal number xxx |
| `\xdd` | Character specified by a hexadecimal number dd |
| `\uxxxx` | The unicode character specified by a hexadecimal number xxxx |

### Quantifiers

| **Modifier** | **Description** |
| --- | --- |
| `n+` | Matches any string that contains at least on n |
| `n*` | Any string that contains zero or more occurrences of n |
| `n?` | A string that contains zero or one occurrences of n |
| `n{X}` | String that contains a sequence of X many n's |
| `n{X,Y}` | String that contains a sequence of X to Y n's |
| `n{X, }` | Matches any string that contains a sequence of at least X n's |
| `n$` | Any string with n at the end of it |
| `^n` | Any string with n at the beginning of it |
| `?=n` | Any string that is followed by a specific string, n |
| `?!n` | Any string that is not followed by a specific string, n |
