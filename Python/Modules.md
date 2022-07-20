# Modules

## Basics

---

Can define/write functions in a script/file and then **import** that script file into another script/file with `import` command

- Referred to as a **module**
- Module file name must end in `.py` extension (otherwise interpreter cannot import)
- When importing, do not include extension

Import default destination will be same file directory as the current file working in that you want to import a module into

- Can also specify different file path

Dictionary of stored modules in a script/file is stored in `sys.modules`

`Sys.path` is a variable located in the sys module containing a few directories:

- Directory of executing script
- List of directories specified by environmental variable `PYTHONPATH`
- Directory where Python is installed

If using a lot of different modules stored in different directories on your computer, can set environmental variable `PYTHONPATH`

- **Environmental variable** is stored by the computer's OS and can be accessed by every program running on the computer
- Can permanently set value of `PYTHONPATH` in the control panel or temporarily via an instance of the command terminal

Can specify names to import from module using `from` keyword

- Example:

        from [module] import [name1], [name2], ...

- Using `import *` will import all objects from a module; not good practice for placing in a script, can get confusing; only use in a single terminable session of the interpreter

When importing whole module, have to access objects in the module with dot notation on the imported namespace

When importing objects from module using from notation, can access objects directly (no dot notation on namespace required)

`Hashlib` standard Python module contains several algorithms for creating secure hash of a text/string message

- Secure hash correlates to single series of characters
- Common hashing algorithms include `md5`, `sha1`, `sha244`

`Import` statement **executes code contained within module**

- Don't treat a module also as a script; only define functions, etc.; don't have code that runs upon importing

\_\_name\_\_ is global string variable automatically added to every module that contains name of module

- For a script `my_funcs.py`, `my_funcs.__name__` would have value of `my_funcs`
- Value of `__name__` for executing script is always set to `__main__` to differentiate executing script from imported modules
- If conditional `if __name__ == __main__:` assessing value of `__name__` on script being executed is true, then the branch is taken
- Contents of a branch taken usually include user interface to functions/class defintions within file

`Reload()` function can be used to re-load & re-execute a module if its contents/source code have been changed

- Reloads a module in-place; when reload([module name]) returns, namespace of module will contain updated definitions
- Importing only objects/attributes from a module by directly calling them with from command will not update/reload module if a reload command is called
- Reloading is typically useful in long-running programs & restarting/reinitializing whole program is expensive/time-consuming

Importing `os` global library as module introduces different system variables/attributes available for use

- Example: ``os.path.getmtime(`module name`.__`file name`__)`` stores the time the module passed was last updated
- ``__`file name`__`` special name contains path to a module in the computer file system

`Package` is a directory that gives access to all modules inside it when imported

- To import, write `import` statement specifying name of directory where package is located
- To indicate directory is a package, must include file called `__init__.py`
- Interpreter will search for package in directories listed in `sys.path`
- Specific subpackages/modules can be imported individually by specifying path to the item (dot notation)

Modules from packages can be imported specifically using from notation like objects from modules

**From notation** summary:

- Using `import x.y.z`: last item `z` must be a package or module
- Using `from w  import x.y.z`: last item `z` can be a package, module, or function/class/global variable

Common standard Python modules:

| **Module** | **Description** |
| --- | --- |
| **datetime** | Creation & editing of dates & time objects |
| **random** | Functions for working with random numbers |
| **math** | Mathematical functions |
| **copy** | Create complete copies of objects |
| **time** | Get current time, convert time zones, sleep for a number of seconds |
| **os** | Operating system informational and management helpers |
| **sys** | System specific environment or configuration helpers |
| **pdb** | Python interactive debugger |
| **urllib** | Url handling functions, such as requesting web pages |
| **hashlib** | Contains algorithms for hasing passwords |
| **matplotlib** | Replicates plotting capability of MATLAB |
| **numpy** | Contains tools for scientific/mathematical computation in Python; required by many other libraries |
| **scipy.stats** | Statistical functions |
| **pandas** | Data frames & statistical functions; tools for reading/writing/subsetting/reshaping data |
| **matplotlib.pyplot** | Data visualization capability |
| **scikit-learn** | Machine learning and data analysis |
| **seaborn** | Data visualization capability |
| **quandl** | Data analysis |

- Can use `as` keyword following an import statement & specify a nickname to thereafter refer to the imported library as for the rest of the script
