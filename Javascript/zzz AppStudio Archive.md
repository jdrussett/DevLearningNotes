# AppStudio Archive

## Events

---

**Events** have three elements:

1. A **named event** for a control (e.g. “`.onclick`”)
2. An **event listener** – a function AppStudio makes that listens for a click on the control
3. An **event handler** – code written that will run when the event happens to the control; the event listener detects the initiation of the control, and runs the control in response

Examples of common control events:

- `.onclick`
- `.mouseover`
- `.onload`
- `.onchange`
- `.onfocusout`

**Radio Buttons** - when you need to pick one from a group. Checkboxes about the same.

- `onclick` - to see if control has been clicked
- `onchange` - to see if one particular radio button has been clicked
- ``addItem(`item`,`type`)``  where `type` is `'selected'` or `'disabled'`; always adds to the end of the list
- `clear()` - clears all item choices
- `items` - items to show, one per line; * disabled, > selected
- `length` - number of items in list
- `value` - index of current selection (starts at 0)

**Dropdown** - shows lists of links; user can pick one (or multiples).

- When the control is initially clicked, an event is sent; When the user makes a selection, onclick is called again with the text of the selection; Can have horizontal or vertical display (property)
- ``addItem(`item`, `type`)`` - type is divider, checked, or disabled
- `clear()` - clears all items
- filter - displays a textbox to filter the items shown
- items - items in the list; * disabled, > selected, - for a line between items, ! for heading
- length - number of items in the list
- selection - the value of the item selected
- value - get/set title of the dropdown button

**Listgroup** - very similar to dropdown; Again, the first click on the control triggers onclick (sending an object); the second click is the selection.

- ``addItem(`item`, `type`, `appearance`)``  where `type` is `'active'` or `'disabled'`; `appearance` is `default`, `success`, `info`, `warning`, `danger`; always adds to the end of the list.
- `clear`() - clears all item choices
- `items` - items to show, one per line; * disabled, > selected
- `length` - number of items in list

**Select** - has a header and footer like many other Bootstrap controls. Shows text that user chooses; developer can also assign behind the scenes values to each choice (eg. a price).

- User can pick multiple items.
  - Use the `.onchange` or `.onfocusout` events.
- Multiselect - have to turn on at design time; Returns selections as an array.
- item(s) - this is the index of chosen item(s); it's an array if user chose more than one item.
- value(s) - this is the non-shown value(s); (like name of a form) of the chosen item(s); it's an array if chose more than one item.
- text - this is the text of the chosen item(s) - it's an array if user chose more than one item.
- ``addItem(`text`, `value`, `selected`, `disabled`)`` - Adds an item with the given text and value to the end of the list; `selected` and `disabled` are boolean.
- `clear()` - clears choices made
- length - number of items on the list
- size - number of rows to display

**Breadcrumbs** - this is a neat feature for navigation. It shows the user how they got to where they are. The crumbs are links to forms.

- uses an array of form names in single quotes (Example: `['form1','form2']`)
- length - number of items in the list of forms
- setValue(array) - resets the list of form names at runtime

**Hamburger** - just like a dropdown control. Two `onclick` events happen when a Hamburger is clicked. When the control is initially clicked, an event is sent. When the user makes a selection, `onclick` is called again with the text of the selection.

- To put a Hamburger on the left, set style to `float:left`; and `align:left`;
- ``addItem(`item`, `type`)`` to add items at runtime
- `clear()`
- items are the menu item text: * for disabled, for selected, ! for heading
- length - number of menu items in menu
- selection - what the user selected

**input** with `inputtype` = date - gives a calendar dropdown on the input box.

**nav** - different ways to have tabs

**modal** - popup you can design

**NSB.MsgBox** is like an alert but specific to AppStudio

## Database Language

---

Basically there are several standard steps to interacting with a database:

1. create a query
2. using ajax call, log into the database and ask a helper program on the database server to run the query and return the results to the program
3. see if the transit trip to the database and back worked or not (returns `200` status code if it worked).
4. if the transit worked, now see if the query worked. To do this, check what was returned (in the `responseText` object). This could be either data (the results of the successful query) or code `500` (if query worked, but there are no results to return, like with a `DELETE`)
5. If transit worked and query worked, now you can do what you need to do with the data

*HINTS* for working with DB scenarios:

1. *** WRITE AN ALGORITHM!
2. copy and paste code from successful forms and adjust to current scenario.
3. you can usually use standard variable names like `req1`, query in each function as they are local to that function
4. best practices: retrieve the data/database when the form is first loaded so you have it to use for the entire project (make it a global variable)

> WRITING QUERIES IN YOUR CODE:
>
> You have to write it so the program will parse it into the correct SQL format for the database.
>
> Example:
>
>     var query = "SELECT * from myStuff"
>     var query = "SELECT firstName from myStuff WHERE firstName =" + '"' + fname + '"'
>     alert(query) to see if it looks correct before you go to the trouble of running it
>
> Together, go to the selectTypeDemo form. We'll look at SELECT first. Make it the first form. Walk through the code and run.

## Using an API

---

1. get an account and an API key from the 'host' - here, the 'host' is Yelp.
2. look at the documentation and find what you want to do.
3. use an example call in the browser from the 'host' API documentation to see what it returns to you and what the format looks like.
4. write the code to make the call.
5. write the code to process the information returned to you - it will be in JSON form that you convert to a Javascript object like an array.

## Yelp Developer Demo

---

1. You already have a Yelp account and API key that you got before class. Go locate your API key on your laptop so you can copy and paste it easily.
2. [Check out the Yelp API documentation](https://www.yelp.com/developers/documentation/v3/get_started)
   1. When you got your Authentication Key, you created an app in your [Yelp dev account](https://www.yelp.com/developers/documentation/v3/authentication)
3. Now test out the API call as well as look at the results returned. Do this by entering this url into the browser (this was in the Yelp API documentation): [https://api.yelp.com/v3/businesses/search?term=coffeeshop&location=omaha](https://api.yelp.com/v3/businesses/search?term=coffeeshop&location=omaha)
   1. Notice that it returns an error - because no authorization key was provided. It needs that to process the request (Yelp keeps track of what you do, makes sure people with no key don't access their services)
4. So add your authorization key. This can't be in the url (security) - it has to be sent as a header in the calling code. Since we are not using code, we will use the tool you installed that will attach a header to the url when it is sent.
5. Add this header to Mod Header tool you installed before class:
   - name: Authorization
   - value: Bearer your API key - like this:
Bearer bvVvExWK3ZXMbJ_jM0MPAPeiiecNksqB0IW0m2rP7TPTXEf7ivv04-lVwk3CUq9ayYsD9OeOZmyngi3LiTgZPrbHgtH9faqasLLAjKtRAhWwWs9ofiK0XZr9cBHzW3Yx
   - open a blank tab in the browser and in Mod Header, click 'lock Tab'- Now Mod Header will add this header code to the API call url of this tab
   - Run the url (hit Return). The results (all the coffee shops in Omaha) will be displayed

        > Note: need Chrome addin 'JSON Formatter' so it is displayed in a nice format.

## Data Table Demo - Employee Data

---

Declare data for data table as array of arrays:

- Example:

        var data1 = [
            ["Tiger Nixon", "System Architect", "Edinburgh", "5421", "2011/04/25", "$320,800"],
            ["Garrett Winters", "Accountant", "Tokyo", "8422", "2011/07/25", "$170,750"],
            ["Ashton Cox", "Junior Technical Author", "San Francisco", "1562", "2009/01/12", "$86,000"],
            ["Cedric Kelly", "Senior Javascript Developer", "Edinburgh", "6224", "2012/03/29", "$433,060"],
            ["Airi Satou", "Accountant", "Tokyo", "5407", "2008/11/28", "$162,700"],
            ["Brielle Williamson", "Integration Specialist", "New York", "4804", "2012/12/02", "$372,000"],
            ["Herrod Chandler", "Sales Assistant", "San Francisco", "9608", "2012/08/06", "$137,500"],
            ["Rhona Davidson", "Integration Specialist", "Tokyo", "6200", "2010/10/14", "$327,900"],
            ["Colleen Hurst", "Javascript Developer", "San Francisco", "2360", "2009/09/15", "$205,500"],
            ["Sonya Frost", "Software Engineer", "Edinburgh", "1667", "2008/12/13", "$103,600"],
            ["Jena Gaines", "Office Manager", "London", "3814", "2008/12/19", "$90,560"],
            ["Quinn Flynn", "Support Lead", "Edinburgh", "9497", "2013/03/03", "$342,000"],
            ["Charde Marshall", "Regional Director", "San Francisco", "6741", "2008/10/16", "$470,600"],
            ["Haley Kennedy", "Senior Marketing Designer", "London", "3597", "2012/12/18", "$313,500"],
            ["Tatyana Fitzpatrick", "Regional Director", "London", "1965", "2010/03/17", "$385,750"],
            ["Michael Silva", "Marketing Designer", "London", "1581", "2012/11/27", "$198,500"],
            ["Paul Byrd", "Chief Financial Officer (CFO)", "New York", "3059", "2010/06/09", "$725,000"],
            ["Gloria Little", "Systems Administrator", "New York", "1721", "2009/04/10", "$237,500"],
            ["Bradley Greer", "Software Engineer", "London", "2558", "2012/10/13", "$132,000"],
            ["Dai Rios", "Personnel Lead", "Edinburgh", "2290", "2012/09/26", "$217,500"],
            ["Jenette Caldwell", "Development Lead", "New York", "1937", "2011/09/03", "$345,000"],
            ["Yuri Berry", "Chief Marketing Officer (CMO)", "New York", "6154", "2009/06/25", "$675,000"],
            ["Caesar Vance", "Pre-Sales Support", "New York", "8330", "2011/12/12", "$106,450"],
            ["Doris Wilder", "Sales Assistant", "Sidney", "3023", "2010/09/20", "$85,600"],
            ["Angelica Ramos", "Chief Executive Officer (CEO)", "London", "5797", "2009/10/09", "$1,200,000"],
            ["Gavin Joyce", "Developer", "Edinburgh", "8822", "2010/12/22", "$92,575"],
            ["Jennifer Chang", "Regional Director", "Singapore", "9239", "2010/11/14", "$357,650"],
            ["Brenden Wagner", "Software Engineer", "San Francisco", "1314", "2011/06/07", "$206,850"],
            ["Fiona Green", "Chief Operating Officer (COO)", "San Francisco", "2947", "2010/03/11", "$850,000"],
            ["Shou Itou", "Regional Marketing", "Tokyo", "8899", "2011/08/14", "$163,000"],
            ["Michelle House", "Integration Specialist", "Sidney", "2769", "2011/06/02", "$95,400"],
            ["Suki Burks", "Developer", "London", "6832", "2009/10/22", "$114,500"],
            ["Prescott Bartlett", "Technical Author", "London", "3606", "2011/05/07", "$145,000"],
            ["Gavin Cortez", "Team Leader", "San Francisco", "2860", "2008/10/26", "$235,500"],
            ["Martena Mccray", "Post-Sales support", "Edinburgh", "8240", "2011/03/09", "$324,050"],
            ["Unity Butler", "Marketing Designer", "San Francisco", "5384", "2009/12/09", "$85,675"]
        ]

Use `JSON.stringify()` to put data in JSON format

- Example:

        var dataJson = JSON.stringify(data1)

Create variable of the desired columns for the data table:

- Example:

        var columns1 = [
            {title: "Name"},
            {title: "Position"},
            {title: "Office"},
            {title: "Extn."},
            {title: "Start date"},
            {title: "Salary", class:"text-right"}
        ]

Useful to create a function to update the table:

- Example:

        function updateTable() {
            dtbEmployees.settings.columns = columns1
            dtbEmployees.settings.data = data1
            dtbEmployees.build()
        }

- Use to refresh and rebuild the table

Function to initially load data table:

- Example:

        function loadTable() {
            var table = $("#dtbEmployees").DataTable()
            table.rows.add(dtbEmployees.settings.data).draw()
        }

- Uses jQuery syntax

Other sample code available in Creighton Archive documents for BIA 375
