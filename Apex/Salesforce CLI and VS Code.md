# Salesforce CLI and VS Code

## Helpful SFDX Commands

---

- `sfdx update` will update salesforce cli to latest version
- `sfdx whatsnew` will show the current release notes for the most recent salesforce cli release
- `sfdx force:org:list` shows all connected orgs
  - Adding `--verbose` to end of command shows more information
- `sfdx force:auth:web:login` authorizes an org
  - To reassign a new org as the default, include `-s` at end of line; the org you login to will become the default
  - Parameter `-r` or `--instanceurl` is instance URL, or specific URL you have to log into org from (i.e. for restricted sandbox)
  - ``--setalias `alias_name` `` sets an alias of the name you provide for the org you're about to log into to authorize
- ``sfdx auth:logout -u `org_alias` `` logs out of an authorized org in VS code/removes it from org list
  - optionally add `-p` flag to avoid having to disable the additional prompt in the console confirming that you want to log out
- `sfdx force --help` provides help on functions syntax
- `sfdx force:doc:commands:list` shows all available sfdx commands
- `sfdx force:alias` manages user name aliases
  - ``sfdx force:alias:set `newAlias`=`username@domain.com` `` will set a new alias for an org with an existing username
- `sfdx commands` lists all commands
- `sfdx force:org:delete` deletes a scratch org tied to a Dev Hub org
  - *Probably* have to specify web address of org (value) or alias given
  - Dev Hub org can only have so many scratch orgs assigned to it, may free up space
- `sfdx force:org:open` automatically opens default scratch org
  - Pass alias at end of line to specify which to open, if not default
- `sfdx force:source:push` pushes all local source code into the default org
- `sfdx force:source:pull` pulls all metadata from default org into local project directory
  - Note: ignores changes made to objects/entities defined in `.forceignore` file (denoted by ``**/`object to ignore` ``)
- ``sfdx force:project:create -n `project_name` `` creates folder called project_name and scaffolds new project with all assets in proper folder structure
  - `-s` option indicates you want a scratch org you create to be default org for project when running SF CLI commands

    > Use different org other than default: specify -u argument and another org alias

  - `-f` option indicates path to the project scratch org configuration file when creating scratch org
- ``sfdx force:data:record:create -s `salesforce object API name` -v `list, in double quotes, of field-value pairs, in single quotes & delimited by a space` `` creates data record in scratch org in given object you specified
- ``sfdx force:data:record:delete -s `salesforce object API name` -w `list, in double quotes, of conditional field values to direct deletion, in single quotes & delimited by a space` `` deletes data record from scratch org from object you specified & according to criteria you specified
- ``sfdx force:data:tree:export -q `SOQL query, in double quotes` --outputdir ./`directory` `` will gather data from default scratch org using query you specified & store it in .json file in directory location you specified
  - can specify `-p` to create a data mapping plan file for queries involving multiple related objects
  - in each object-specific section of JSON within the plan.json file:
  
    > - mark `saveRefs` as `true` if *other* related object records need to find these records as lookup references
    > - mark `resolveRefs` as `true` if *these* object records need to find lookup references to other related object ids

- ``sfdx force:data:tree:import --sObjectTreeFiles `directory`/`.json file(s)` -u  `destination org alias` `` will import data into default scratch org pulled from data source specified with directory and `.json` file

  - alternatively, can execute command with `-p` flag to deploy data according to a data mapping plan which references several other data files in JSON format

  > a data mapping plan file might look like this:
  >
  >     [
  >       {
  >         "sobject": "Candidate__c",
  >         "saveRefs": true,
  >         "resolveRefs": false,
  >         "files": [
  >           "Candidate__cs.json"
  >         ]
  >       },
  >       {
  >         "sobject": "Candidate_History__c",
  >         "saveRefs": false,
  >         "resolveRefs": true,
  >         "files": [
  >           "Candidate_History__cs.json"
  >         ]
  >       }
  >     ]
  >
  > ... provided the object records reference each other correctly with placeholder IDs/references

- ``sfdx force:apex:class:create -n `class/controller name` -d `directory location` `` creates new apex class with given name in given directory location
- ``sfdx force:lightning:event:create -n `event name` -d `directory location` `` creates new aura event with given name in given directory location
- ``sfdx force:lightning:component:create -n `aura component name` -d `directory location` `` creates new aura component bundle with given name in given directory location
- ``sfdx force:org:create -f config/project-scratch-def.json -a `org name` `` creates a new scratch org with given name
- ``sfdx force:user:permset:assign -n `name of permission set` -u `name of org` `` assign a permission set to default user in a scratch org/specified org
- ``sfdx force:org:display -u `org name` `` will show configuration data for an org you specify
- ``sfdx force:user:password:generate -u `org name` `` will automatically generate random strong password for default user for org you specify (scratch only?)
- ``sfdx force:mdapi:convert -r `folder containing metadata`/`` converts all metadata into source format, stores in default folder location
- `sfdx force:package:create` creates new Salesforce DX package

    > Can specify:
    >
    > - Package name following `--name`
    >   - Name becomes alias you can use when running subsequent packaging commands
    > - Package description following `--description`
    > - Package type following `--packagetype` ('Unlocked', for example)
    > - Package file/directory path following `--path` (commonly 'force-app')
    >   - Will contain the contents of the package
    > - Package namespace following `--namespace` (or indicate no namespace with `--nonamespace`)
    > - Package target development hub following `--targetdevhubusername`

- `sfdx force:package:list` view all created packages in the current designated default dev hub
- `sfdx force:package:version:create` creates package version, associating metadata w/ package

    > Can specify:
    >
    > - Package alias that maps to package ID following `-p`
    > - Directory containing package contents following `-d`
    > - Installation key protecting package from being installed by unauthorized individuals following `-k`

- ``sfdx force:package:version:promote -p `package name` -v `development hub org alias` `` promote a package to "released" status
- `sfdx force:source:retrieve` retrieves metadata from org & saves it in local repository
  - Specify ``-u `sandbox_name` `` and ``-m ApexClass:`class_name` `` to push particular class
  - For multiple Apex classes at once, surround in quotes & separate by commas
  - Example:

        sfdx force:source:retrieve -u `sandbox_name` -m "ApexClass:`class_name1`, ApexClass:`class_name2`"

  - Executing simply ``sfdx force:source:retrieve -u `sandbox_name` -m ApexClass`` will retrieve all Apex class from org at once
  - ``sfdx force:source:retrieve -u `sandbox_name` -x ./package.xml`` will retrieve the metadata referenced in a `package.xml` file from the org and add the metadata files to the `force-app` folder
- `sfdx force:source:deploy` pushes metadata from local repository to Salesforce org
  - Specify ``-u `sandbox_name` `` and ``-m ApexClass:`class_name` `` to push particular class
  - For multiple Apex classes at once, surround in quotes & separate by commas
  - Example:

        sfdx force:source:deploy -u `sandbox_name` -m "ApexClass:`class_name1`, ApexClass:`class_name2`"

  - Executing simply ``sfdx force:source:deploy -u `[sandbox_name]` -m ApexClass`` will deploy all Apex class to org at once
  - Add flag `--checkonly` to validate a deployment without committing the code to the org
  - To deploy destructive changes, create a folder called 'destructive' at the highest/root level within the project. In the destructive folder, create two files:
    - `destructiveChanges.xml`, which is structured exactly like a typcial package.xml file and contains the *content that you want to delete*
    - `package.xml` which is a **blank package.xml file that will only contain the following contents** (with whatever current version of the API you are using)

          <?xml version="1.0" encoding="UTF-8"?>
          <Package xmlns="https://soap.sforce.com/2006/04/metadata">
            <version>52.0</version>
          </Package>

  - To deploy the destructive change, run the following command once you have the correct metadata contents defined in your destructiveChanges.xml file: `sfdx force:mdapi:deploy --deploydir .\destructive --targetusername org_alias`
  - `sfdx force:limits:api:display` allows you to view your org's metadata limits for working with sfdx/dev ops model

## Flags & Abbreviations

---

| **Abbreviated Flag** | **Full Flag Name** | **Command Usage** |
| --- | --- | --- |
| `-q` | `--query` | force data tree exports or imports |
| `-u` | `--targetusername` | any command that affects a Salesforce org |
| `-r` | `--instanceurl` | authenticating to a new org |
| `-m` | `--metadata` | force source deploy or retrieve |
| `-f` | `--sobjecttreefiles` | force data tree exports or imports |
| `-p` | `--plan` | force data tree exports or imports |
| `-d` | `--outputdir` | force data tree exports |

## VS Code

---

- Command palette tricks (summon with Ctrl + Shift + P):
  - SFDX: Get Apex Debug Logs
  - SFDX: Execute Anonymous Apex with Editor Comments
  - SFDX: Create a Project
  - Terminal: Select Default Shell
- Right-click on classes, click deploy source to org (set org default first)
- **Apex replay debugger**: first turn on debugging, then run apex tests, get debug logs, set breakpoints/checkpoints in code, open apex replay debugger with current log file, all that stuff

    > Check out trailhead module on apex replay debugger for more help  

- **Terminal > Integrated: Cwd** is the setting that specifies the default directory/file path when you open a terminal in VS Code
- **Salesforcedx-vscode-apex > Java: home** is the path where your java runtime is installed to launch the Apex Lanugage Server (needed for apex replay debugger)

### Keyboard Shortcuts

| **Keyboard Shortcut** | **Function** |
| --- | --- |
| `Ctrl + /` | comments out a line of Apex in VS Code |
| `Ctrl + Shift + K` | deletes line |
| `Ctrl + Alt + Arrow up or down` | Expands cursor to multiple lines |
| `Ctrl + Shift + Arrow up or down` | Copies the line/lines you're on and pastes below |

## Git Commands

---

- ``git clone `[web address of github project]` `` will clone a git project & store it in a folder in the current dx project file folder location

## Other CLI Miscellaneous Content

---

- `-d` parameter makes it a default org
- `-a` gives org/object an alias
- Adding `-help` after any sfdx command will display the help documentation for that command; information on the command's function, descriptions of each parameter, short & long versions of each parameter
- `--verbose` at end of command shows more information (`sfdx force:org:list` only?)
- `-s` option indicates you want a scratch org you create to be default org for project when running SF CLI commands
  - Use different org other than default: specify `-u` argument and another org alias
- `-f` option indicates path to the project scratch org configuration file when creating scratch org
- ``mkdir `directory name` `` creates a directory/folder within current project directory
