# Shane Young YouTube Series

Video Archive:

- [Microsoft Powershell for Beginners - Video 1 Learn Powershell](https://www.youtube.com/watch?v=IHrGresKu2w)
- [Maniuplating Objects in Microsoft Powershell - Video 2](https://www.youtube.com/watch?v=f9xPJXslVWE)

## Microsoft PowerShell for Beginners - Video 1 Learn PowerShell

---

### Core Ideas

1. Powershell is a language that returns objects as opposed to simply text, like a generic command prompt.
2. Variables in PowerShell are always prefaced with a `$`
   - Variable definition is as straightforward as a generic assignment statement; e.g. `$MSEdge = Get-Process MicrosoftEdge`
   - Check the definition of a variable by simply passing the name of the variable to the console
   - Access methods and properties of variables with dot notation just like you would for the actual objects
     - i.e. `[Object_Name].[Method_or_property]`
3. Commands are stacked/executed with each other via **piping mechanism**, *similar to coding in **R***
   - When piping an object into another command/destination, the phrase `$_.` represents the current object in the pipe loop
   - Command to which collection object is piped automatically iterates through collection of objects that was piped to it
4. Flags can be used in commands for things like expressions/comparisons
   - For example, the flag `-gt` stands for "greater than"
5. Passing some text enclosed in double quotes to the terminal will simply print that text in the terminal
6. Any time you want to manipulate one of your output objects (such as dividing free space number to get it out of bytes unit of measurement) always have to **surround your manipulation in parentheses**
7. A semicolon `;` is needed to puncuate each individual line of Powershell code

### Properties

| **Property** | **Property Description/Function** |
| --- | --- |
| `free` | Returns remaining free space of the object; always outputs in bytes, but supports division to get to kilo-/mega-/giga-bytes; can use `[object].free/1024/1024/1024` or `[object].free/1gb` to get to gigabytes |
| | |

### Operators and Wildcards

| **Operator Key** | **Operator Name** | **Operator Function** | **Example** |
| --- | --- | --- | --- |
| `\|` | Pipe operator | propogates the result of one command to another command/destination | `Get-Process -Name` *[`Process_Name`]* `\| Get-Member` will return a list of all properties, events, methods, etc. of a given process that you provide |
| `*` | "All" wildcard | Returns all possible objects/items of interest, like in SQL | `Get-PSDrive \| Select-Object *` |
| `$` | Variable assignment operator | Tells powershell to assign the variable a value of whatever is passed following the equals sign `=` | `$pi=3.14159265` or `$myName=Jake` |

### Flag Operators

| **Flag** | **Flag Function** |
| --- | --- |
| `-gt` | Greater than |
| `-cgt` | |
| `-ge` | Greater than or equal to |
| `-cge` | |
| `-lt` | Less than |
| `-clt` | |
| `-le` | Less than or equal to |
| `-cle` | |
| `-ceq` | |
| `-ne` | Not equal to (?) |
| `-cne` | |
| `-like` | |
| `-clike` | |
| `-notlike` | |
| `-cnotlike` | |
| `-match` | |
| `-cmatch` | |
| `-notmatch` | |
| `-cnotmatch` | |
| `-contains` | |
| `-ccontains` | |
| `-notcontains` | |
| `-cnotcontains` | |
| `-in` | |
| `-cin` | |
| `-notin` | |
| `-cnotin` | |
| `-is` | |
| `-isnot` | |
| `-Foregroundcolor` | Changes the color of the output text that is printed in the terminal as a result of whatever command is run |
| | |

### Built-in Aliases To Remember

| **Alias Key/Name** | **Command Alias Executes** |
| --- | --- |
| `?` | `Where-Object` |
| `%` | `ForEach-Object` |
| `h` | `Get-History` |
| `r` | `Invoke-History` |

### Helpful commands

> Keep in mind:
>
> - All commands in powershell are formatted as [`verb`]-[`noun`]
> - Powershell supports wildcarding with asterisks

- `Start-Transcript` --  this will begin a transcript of the session that you can go back and review to see what commands you ran in the session of powershell
  - Will generate the file in your documents folder by default; run `Get-Help Start-Transcript` or `Get-Help Start-Transcript -Examples` to see how to manipulate the file path destination
- `Get-Command` -- lists *all* commands available in Powershell
  - good practice to add some qualifiers after so it doesn't take a long time to print out every command available in all of powershell...
  - e.g.: can supply `Get-Command -noun S*` to retrieve all commands whose noun component begins with an "s"
  - `Get-Command -noun Service` will retrieve all powershell commands whose noun is "service"
- `Get-Help` *[`command`]*-*[`name`]* will provide help on whatever command name is supplied
  - `Get-Help` *[`command`]*-*[`name`]* `-Examples` will list examples of the command used (fair warning that examples are crowd-sourced, not all may be accurate)
  - `Get-Help` *[`command`]*-*[`name`]* `-Online` will take you to online documentation for the command supplied

> Some Powershell commands have aliases that can be used as shortcuts to run the commands
>
> - e.g. `cls` is really short-hand for `Clear-Host`

- `Get-Alias` will supply the command names for *all* aliases known to the system
- `Get-Alias` *[`alias`]* will provide the full command name for the alias supplied
- `Get-Process` will return a list of all processes running on the machine, similar to Task Manager
- `Get-History` will return a list of all commands run in the history of the current session
- `Get-PSDrive` will return all the drives on your system and their existing free space
- `Where-Object` filters the returned objects by a condition you pass it, surrounded in curly brackets `{}`
- ``Select-Object `[Object_Name]` `` returns only the selected objects (of an object that is piped into the command, for example) that you specify
  - can specify multiple object names, separated by commas
  - e.g. `Get-PSDrive | Select-Object Name` will return a list of the names of drives on your computer
- `ForEach-Object` **loops** through the object collection passed to it and executes the proceeding command enclosed in curly brackets `{}` for each object it processes
  - You can have up to three sets of curly brackets to indicate an initialization behavior, a loop behavior, and a final/completion behavior

        ForEach-Object 
          { this code will be executed once before the loop begins }
          { this code will be executed for each time through the loop }
          { this code will be executed after the last iteration of the loop }

- `Write-Host` writes/prints whatever is provided after it to the terminal
  - if you want to change the color of the texted printed to the terminal, you have to use `Write-Host`!

> [A helpful article to understand a simple .NET number formatting tool that can make your numbers look nicer when they are processed/output in Powershell](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-powershell-1.0/ee692795(v=technet.10)?redirectedfrom=MSDN)

- `Get-Volume` returns some basic OS information about the drive you're currently on in the terminal
