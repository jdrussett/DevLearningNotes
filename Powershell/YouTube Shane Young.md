# Microsoft PowerShell for Beginners - Video 1 Learn PowerShell

Link to video: [Click Here](https://www.youtube.com/watch?v=IHrGresKu2w)

## Ideas

1. Powershell is a language that returns objects as opposed to simply text, like a generic command prompt.
2. We can use the pipe operator `|` to 'pipe' the resulting object from one command to another command/destination  
   - e.g. `Get-Process -Name` *[`ProcessName`]* `| Get-Member` will return a list of all properties, events, methods, etc. of a given process that you provide
3. Variables in PowerShell are always prefaced with a `$`
   - Variable definition is as straightforward as a generic assignment statement; e.g. `$MSEdge = Get-Process MicrosoftEdge`
   - Check the definition of a variable by simply passing the name of the variable to the console
   - Access methods and properties of variables with dot notation just like you would for the actual objects

## Helpful commands

> Keep in mind:
>
> - All commands in powershell are formatted as [`verb`]-[`noun`]
> - Powershell supports wildcarding with asterisks

[ ----- start of list ----- ]: #

- `Start-Transcript` --  this will begin a transcript of the session that you can go back and review to see what commands you ran in the session of powershell
  - Will generate the file in your documents folder by default; run `Get-Help Start-Transcript` or `Get-Help Start-Transcript -Examples` to see how to manipulate the file path destination
- `Get-Command` -- lists *all* commands available in Powershell
  - good practice to add some qualifiers after so it doesn't take a long time to print out every command available in all of powershell...
  - e.g.: can supply `Get-Command -noun S*` to retrieve all commands whose noun component begins with an "s"
  - `Get-Command -noun Service` will retrieve all powershell commands whose noun is "service"
- `Get-Help` *[`command`]*-*[`name`]* will provide help on whatever command name is supplied
  - `Get-Help` *[`command`]*-*[`name`]* `-Examples` will list examples of the command used (fair warning that examples are crowd-sourced, not all may be accurate)
  - `Get-Help` *[`command`]*-*[`name`]* `-Online` will take you to online documentation for the command supplied

> some Powershell commands have aliases that can be used as shortcuts to run the commands
>
> - e.g. `cls` is really short-hand for `Clear-Host`

- `Get-Alias` will supply the command names for *all* aliases known to the system
- `Get-Alias` *[`alias`]* will provide the full command name for the alias supplied
- `Get-Process` will return a list of all processes running on the machine, similar to Task Manager
- `Get-History` will return a list of all commands run in the history of the current session

[ ----- end of list ----- ]: #
