# Interacting with Files

## Basics

---

- `Open()` is built-in function used to get input from a file
  - Requires single argument that specifies path to file
- `` `file name`.close()`` method closes the file, after which no more reads or writes on it are allowed in the executing script
- `` `file name`.read()`` method returns the whole file's contents as a string
  - Optional argument to specify number of bytes to read from the file
- `` `file name`.readlines()`` method returns a list of the lines of a file as string elements
  - Optional argument to specify number of bytes to read from the file
- `` `file name`.readline()`` returns one line of a file at a time
- `` `file name`.write()`` method writes a string argument to a file
  - *Only* accepts string arguments; convert numeric type to data to string before writing to file
  - When writing to a file, mode of file must be set in `open()` function call; `mode` indicates how file is opened (whether writing to file is allowed, whether existing contents are overwritten/appended to, etc.)
    - Mode is specified as second argument (after file name) in `open()` function call
    - Example:

            file_variable = open('`file_name.txt`', 'r')

Different modes for opening files include:

| **Mode** | **Basic Function** | **More Detail** |
| --- | --- | --- |
| `r` | Open file for reading | Only allows reading; does not allow writing, creating, or overwriting file |
| `w` | Open file for writing; if file does not exist, it is created; contents of existing file are overwritten | Allows writing, overwriting, or creating new file; does not allow reading file |
| `a` | Open file for writing; if file does not exist, it is created | Allows writing, creating, or appending to file; does not allow reading or overwriting contents of existing file |

> Note: can also add `+` after letter character specifying mode of file open to specify update mode; allow both reading and writing to file at the same time

- Interpreter enacts a **buffer** for output to a file being written as data on the computer's hard drive; by default data is line-buffered
  - Data written to drive (only) when newline character is output to the file & read by the interpreter (by default)
  - Can toggle buffering on/off or set size of buffer with optional `buffering=` argument to `open()` function call
    - Passing `0` disables buffering (only available for binary files…)
    - Passing `1` sets buffer to default line-buffering
    - Passing anything greater than 1 sets byte size of each buffer
- `.flush()` method forces interpreter to flush output buffer to disk
- To operate with file system through standard Python-supported functionality, import `os` module
- Path separators are the characters that separate subdirectories/locations in a file location path for an operating system (`\\` on Windows, `/` on Mac OS)
  - To increase portability/avoid hardcoding a file path to a file in a script, can us `os.path` module, containing portable functions for handling file paths
    - `os.path.join()` concatenates arguments using correct path separator for current operating system; pass each new subdirectory/folder as new argument to the function
    - Example:

            "C:/Users/Jake Russett/Documents/Jake/Creighton/aa BIA 479/my_file.txt" --> os.path.join('C:\\', 'Users', 'Jake Russett', ... 'my_file.txt')

    > Note: on Windows, if specifying the entirety of the path, starting with drive letter (C:) have to inlcude separator with the drive letter in the os.path.join() function, as seen above

  - `os.path.sep` stores path separator for current operating system, so it can be used to split a file path in string form into individual path/directory elements
  - Example:

            tokens = 'C:\\Users\\Jake Russett\\Documents\\Jake\\my_file.txt'.split(os.path.sep)

Other helpful functions contained in os and os.path modules:

| **Function** | **Description** |
| --- | --- |
| ``os.path.split(`path`)`` | Splits passed path into 2-tuple ``(`head`, `tail`)`` where tail is last token in the path string & the head is everything else |
| ``os.path.exists(`path`)`` | Boolean function that returns `True` if the passed file path exists and `False` if it doesn't
| ``os.path.isfile(`path`)`` | Boolean function that returns `True` if the passed file path is a file and `False` if it isn't |
| ``os.path.getsize(`path`)`` | Returns size of the passed path in bytes |

- `os.walk()` function 'walks' a directory tree/structure and visits each subdirectory in the specified path
  - Used as an iterable object in a for loop that yields a 3-tuple for every iteration:
    1. First item is the path to the current directory
    2. Second item is a list of all subdirectories of the current directory
    3. Third item is a list of all files residing in the current directory

- `with` statement can be used to open a file, execute a block of statements, and automatically close file when statements are complete/have run
  - Format: ``with open(`file_name`, '[r]/[w]/[a][+]') as `file`:``
  - Statement creates `context manager` to manage usage of the resource by automatically performing "setup & teardown" operations
- Python standard library/module `csv` can be used to help read/write files in the csv format
  - To read file using `csv` module, have to create **reader object** using `csv.reader()` function & passing a file object created using `open()` function and specifying delimiting character (almost always a comma for csv files)
  - Example:

        with open('mycsv.csv', 'r') as csvfile:
        read_csv = csv.reader(csvfile, delimiter = ",")

  - Reader object stores csv data as a list of lists (a list of m many lists, where each list contains `n` elements --> `m` rows by `n` columns)

> *Clever trick*: write a loop to iterate one time with only a `continue` statement within the `with` statement in a file to ignore the first/header row in the csv file

- Can also use `csv` module to write text into a csv file using a **writer object**
  - `.writerow()` and `.writerows()` methods on a writer object (using `csv.writer()` function & passing file object created using `open()` function & specifying delimiting character) can be used to write a list of strings into the file as one or more rows
    - Pass a list of strings to `.writerow()` method, all same length as the number of columns in the csv, or pass list of lists of strings to `.writerows()`
