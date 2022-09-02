# PHP

## Ten Steps For Using PHP With MySQL

---

> **The ten steps**:
>
> 1. Write code for HTML
> 2. Write code for PHP
> 3. Write code for separate files to include
> 4. Connect to MySQL
> 5. Include other files if necessary & close connections
> 6. Create query & execute it
> 7. Free the results
> 8. Fetch the results (select statements only)
> 9. Display the results (select statements only)
> 10. Write code for CSS

### Step 1

    <!doctype html> --indicates the file is of type HTML
    <html> --indicates start of HTML code 
        <body> --indicates where main page begins; stores text of entire document
            <div class="class_type(?)"> --a container
                <h4>header text</h4> --indicates font style & size
                <div class="class_type(?)"></div>
            </div>
        </body>
    </html>

- `<div>`: elements that serve as a division of the page; use CSS to format these later

### Step 2

    <?php
    ?>
    <!doctype html>
    <html>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
            </div>
        </body>
    </html>

### Step 3

    define('MyDB_HOST', 'name of host server; i.e. IP address');
    define('MyDB_USER', 'user username');
    define('MyDB_PASSWORD', 'user password');
    define('MyDB_NAME', 'schema name');

- All these located in a separate PHP file, perhaps called "db.php"
- Putting these into a separate file allows us to establish a connection with other files & then just simply reference the name of this file instead of typing the same code over and over again when needed

### Step 4

    define('MyDB_HOST', 'name of host server; i.e. IP address');
    define('MyDB_USER', 'user username');
    define('MyDB_PASSWORD', 'user password');
    define('MyDB_NAME', 'schema name');
    $con = mysqli_connect(MyDB_HOST, MyDB_USER, MyDB_PASSWORD, MyDB_NAME) or exit("Connection failed: [or other generic error message]" . mysqli_connect_error());

- All these located in a separate PHP file, perhaps called "db.php"
- Putting these into a separate file allows us to establish a connection with other files & then just simply reference the name of this file instead of typing the same code over and over again when needed

### Step 5

    <?php
        require_once("separate php file name  with connection definitions");
        some other php code
        mysqli_close($con);
    ?>
    <!doctype html>
    <html>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
            </div>
        </body>
    </html>

- Here, the "separate php file name" might be "db.php" as mentioned earlier

### Step 6

    <?php
        require_once("separate php file name  with connection definitions");
        $query = "SELECT ...
                  FROM schema.table
                  WHERE ...
                  ... ;";
        $results = mysqli_query($con, $query) or die(
            "Query failed: [or other generic error message]" . mysqli_error($con)
        );
        mysqli_close($con);
    ?>
    <!doctype html>
    <html>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
            </div>
        </body>
    </html>

- `$` defines a variable in PHP; something (an object) that is used multiple times with different parameters, etc.

### Step 7

    <?php
        require_once("separate php file name  with connection definitions");
        $query = "SELECT ...
                  FROM schema.table
                  WHERE ...
                  ... ;";
        $results = mysqli_query($con, $query) or die(
            "Query failed: [or other generic error message]" . mysqli_error($con)
        );
        mysqli_free_result($results);
        mysqli_close($con);
    ?>
    <!doctype html>
    <html>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
            </div>
        </body>
    </html>

- `mysqli_free_result()` clears variable results so it is free to be reused & doesn't have any unwanted lingering data

### Step 8

    <?php
        require_once("separate php file name  with connection definitions");
        $query = "SELECT ...
                  FROM schema.table
                  WHERE ...
                  ... ;";
        $results = mysqli_query($con, $query) or die(
            "Query failed: [or other generic error message]" . mysqli_error($con)
        );
        while ($row = mysqli_fetch_array($results)) {
            ...
        }
        mysqli_free_result($results);
        mysqli_close($con);
    ?>
    <!doctype html>
    <html>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
            </div>
        </body>
    </html>

- `while ($row = mysqli_fetch_array($results) { ... }` creates row to serve as structure to store results of row variable; while loop allows code to re-execute for as many rows as necessary

### Step 9

    <?php
        require_once("separate php file name  with connection definitions");
        $content = "";
        $query = "SELECT ...
                  FROM schema.table
                  WHERE ..
                  ... ;";
        $results = mysqli_query($con, $query) or die(
            "Query failed: [or other generic error message]" . mysqli_error($con)
        );
        $content .= "<table>";
        $content .= "<tr><th>column1_name</th>
                         <th>column2_name</th>
                         <th>column3_name</th>
                         ... . . . . . . . ...
                     </tr>";
        while ($row = mysqli_fetch_array($results)) {
            $content .=  "<tr><td>{$row['db_column1']}</td>
                              <td>{$row['db_column2']}</td>
                              <td>{$row['db_column3']}</td>
                              ... . . . . . . . . . . . ...
                          </tr>";
        }
        $content .= "</table>";
        mysqli_free_result($results);
        mysqli_close($con);
    ?>
    <!doctype html>
    <html>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
                <div class="results"><?php echo $content; ?></div>
            </div>
        </body>
    </html>

### Step 10

    <?php
        require_once("separate php file name  with connection definitions");
        $content = "";
        $query = "SELECT ...
                  FROM schema.table
                  WHERE ...
                  ... ;";
        $results = mysqli_query($con, $query) or die(
            "Query failed: [or other generic error message]" . mysqli_error($con)
        );
        $content .= "<table>";
        $content .= "<tr><th>column1_name</th>
                         <th>column2_name</th>
                         <th>column3_name</th>
                         ... . . . . . . . ...
                     </tr>";
        while ($row = mysqli_fetch_array($results)) {
            $content .=  "<tr><td>{$row['db_column1']}</td>
                              <td>{$row['db_column2']}</td>
                              <td>{$row['db_column3']}</td>
                              ... . . . . . . . . . . . ...
                          </tr>";
        }
        $content .= "</table>";
        mysqli_free_result($results);
        mysqli_close($con);
    ?>
    <!doctype html>
    <html>
        <head><link href="CSS file name" rel="stylesheet"></head>
        <body>
            <div class="class_type(?)">
                <h4>header text</h4>
                <div class="class_type(?)"></div>
                <div class="results"><?php echo $content; ?></div>
            </div>
        </body>
    </html>

## Query With Forms

**Querying using forms**: rather than show static information on web page, going to show/return information supplied by user

1. Enter form structure in body tag in `HTML` code

        <!-- PHP code above -->
        ?>
        <body>
        <h4>...</h4>
        <form method="post"  action="php file destination name">
            <input type="text" name="name of textbox">
            <input type="submit" name="submit">
        </form>
        <!-- rest of HTML code below -->

    - method="post" defines method of response to user interaction
    - "php file destination name" identifies location of posted values of form; optional if referencing current page
    - "name of textbox" is whatever someone types into the textbox; variable name is equal to entered value of textbox
    - Input of type "submit" generates submit button for a textbox

2. Create `IF` statement to run code off user interaction

        <?php
        $content .= "";
        if (isset($_POST['submitname'])) {
            require_once("separate PHP file name");
            ... query, table/results construction, etc. ...
            mysqli_close($con);
        }

   - `submitname` here MUST MATCH name of the submit input type

3. Query using value user provided in interactive textbox

        <!-- PHP code above -->
        require_once("separate php file name");
        $name_of_textbox = $_POST['name of textbox'];
        $query = "SELECT ...
                  ...
                  WHERE name_of_textbox = '$name_of_textbox';";
        $results = mysqli_query(….);
        <!-- PHP code below -->

    - Whatever identified in textbox is stored in posted variable
    - `name of textbox` variable defined is input specified by user in textbox
    - `WHERE name_of_textbox = '$name_of_textbox'` object defined by user in the textbox should be a column in the database

## Using Forms and Results Pages

---

- Separating forms into form & results pages: will require 2 separate pages/files

        <!doctype html>
        <html>
            <head><link href="CSS file name" rel="stylesheet"></head>
            <body>
                <div class="container">
                    <hsmall_positive_integer>header text</hsmall_positive_integer>
                         <form method="post"  action="php file destination name">
                             <input type="text" name="name of textbox">
                             <input type="submit" name="submit">
                         </form>
                         <!-- more HTML code below -->
                </div>
            </body>
        </html>

  - No PHP code contained on this page
  - "php file destination name" will be the name of the results page
- Results page will look like:

        <!-- PHP code above -->
        <!doctype html>
        <html>
            <head><link href="CSS file name" rel="stylesheet"></head>
            <body>
                <div class="container">
                    <hsmall_positive_integer>header text</hsmall_positive_integer>
                    <div class="results"><?php $content; ?></div>
                </div>
            </body>
        </html>

- **In a nutshell**: splitting one page with a form into two pages... new pages contains just HTML code with form elements included, and references results page & does not include "echo $content" statement; this becomes the form page; on the original page, delete the form elements from HTML code, keep the PHP code & "echo $content" statement, & this becomes the results page

## Other Stuff

---

### Populating A Dropdown Menu

> *Useful because you can restrict the types of values users are allowed to enter*

        <?php
            require_once("separate php file name");
            $content = "";
            $query = "this query will determine how the dropdown is populated";
            $results = mysqli_query($con, $query) or die(
                "Query failed: [or other generic error message]" . mysqli_error($con)
            );
            $content .= "<table>";
            while ($row = mysqli_fetch_array($results)) {
                $content .= "<option value='{$row["value submission column name"]}'>
                                            {$row['value selection column name']}
                             </option>";
            }
            mysqli_free_result($results);
            <!-- rest of PHP code -->
        ?>
        <!doctype html>
        <html>
            <body>
                <h4>header text</h4>
                <form method="post" action="php file destination name">
                    <div><label for="column_name (name of textbox)">dropdown menu caption</label>
                        <select name="column_name">
                            <?php echo $content; ?>
                        </select>
                    </div>
                </form>
            </body>
        </html>

- `$content .= "<option ...>"` --- putting results into options instead of table
- `value submission column name` --- information passed to database/results page; typically the ID/primary key field
- `value selection column name` --- information user will see & select from; typically a name/description field understandable to the user

### Types of input for HTML

- Type of submit: `<input type="submit" ... >` --- create submit button
- Type of text: `<input type="text" ... >` --- create textbox
Type of select: `<select ... >` --> create dropdown
