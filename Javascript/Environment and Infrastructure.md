# Environment and Infrastructure

## Javascript as Scripting

---

Include Javascript in an HTML page:

    <script type="text/javascript">
        // Javascript code…
    </script>

Call an external Javascript file:

    <script src="myscript.js"></script>
    <code>
        code goes here
    </code>

## DOM Mode

---

[Information about DOM: Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)

### Node Properties

- `attributes` returns live collection of all attributes registered to an element
- `baseURI` provides absolute base URL of an HTML element
- `childNodes` gives collection of an element's child nodes
- `firstChild` returns first child node of an element
- `lastChild` returns last child node of an element
- `nextSibiling` returns next node at same node tree level
- `nodeName` returns the name of a node
- `nodeType` returns the type of a node
- `nodeValue` returns or sets the value of a node
- `ownerDocument` is the top-level document object for the current node
- `parentNode` returns the parent node of an element
- `previousSibilng` returns the node immediately preceding the current one
- `textContent` returns or sets the textual content of a node & its descendants

### Node Methods

- `appendChild()` adds a new child node to an element as the last child node
- `cloneNode()` clones at HTML element
- `compareDocumentPosition()` compares the document position of two elements
- `getFeature()` returns an object which implements the APIs of a specified feature
- `hasAttributes()` returns true if an element has any attributes
- `hasChildNodes()` returns true if an element has any child nodes
- `insertBefore()` inserts a new child node before a specified, existing child node
- `isDefaultNamespace()` returns true if a specified namespaceURI is the default, otherwise false
- `isEqualNode()` checks if two elements are equal
- `isSameNode()` checks if two elements are the same
- `isSupported()` returns true if a specified feature is supported on the element
- `lookupNamespaceURI()` returns namespaceURI associated with a given node
- `lookupPrefix()` returns DOMString containing the prefix for a given namespaceURI if present
- `normalize()` joins adjacent text nodes and removes empty text nodes in an element
- `removeChild()` removes a child node from an element
- `replaceChild()` replaces a child node in an element

### Element Methods

- `getAttribute()` returns specified attribute value of an element node
- `getAttributeNS()` returns string value of the attribute with the specified namespace and name
- `getAttributeNode()` gets the specified attribute node
- `getAttributeNodeNS()` returns attribute node for the attribute with the given name and namespace
- `getElementsByTagName()` provides collection of all child elements with the specified tag name
- `getElementsByTagNameNS()` returns a live HTMlcollection of elements with a certain tag name belonging to the given namespace
- `hasAttribute()` returns true if an element has any attributes, otherwise false
- `hasAttributeNS()` returns a boolean value indicating whether the current element in a given namespace has the specified attribute
- `removeAttribute()` removes specified attribute from an element
- `removeAttributeNS()` removes specified attribute from an element within a certain namespace
- `removeAttributeNode()` takes away a specified attribute node and returns removed node
- `setAttribute()` sets or changes the specified attribute to a specified value
- `setAttributeNS()` adds a new attribute or changes the value of an attribute with the given namespace and name
- `setAttributeNode()` sets or changes the specified attribute node
- `setAttributeNodeNS()` adds a new namespaced attribute node to an element

## Working With the User Browser

---

### Window Properties

- `closed` returns boolean value indicating whether a window has been closed or not
- `defaultStatus` sets or returns default text in the status bar of a window
- `document` returns the document object for the window
- `frames` returns all `<iframe>` elements in the current window
- `history` provides History object for the current window
- `innerHeight` inner height of a window's content area
- `innerWidth` inner width of a window's content area
- `length` returns the number of `<iframe>` elements in the current window
- `location` returns the location object for the window
- `name` sets or returns the name of a window
- `navigator` returns the navigator object for a window
- `opener` returns a reference to the window that created the current window
- `outerHeight` outer height of a window including scrollers/toolbars
- `outerWidth` outer width of a window including scrollers/toolbars
- `pageXOffset` returns number of pixels the current document has been scrolled horizontally
- `pageYOffset` returns number of pixels the current document has been scrolled vertically
- `parent` the parent window of the current window
- `screen` returns the screen object of the current window
- `screenLeft` returns the horizontal coordinate of the window, relative to the screen
- `screenTop` returns the vertical coordinate of the window
- `screenX` is same as screenLeft but needed for some browsers
- `screenY` is same as screenTop but needed for some browsers
- `self` returns the current window
- `status` sets or returns the text in the statusbar of a window
- `top` returns the topmost browser window

### Window Methods

- `alert()` displays an alert box with a message and an OK button
- `blur()` removes focus from the current window
- `clearInterval()` clears a timer set with setInterval()
- `clearTimeout()` clears a timer set with setTimeout()
- `close()` closes current window
- `confirm()` displays a dialogue box with a message and an OK an cancellation button
- `focus()` sets focus to the current window
- `moveBy()` moves a window relative to its current position
- `moveTo()` moves a window to a specified position
- `open()` opens a new browser window
- `print()` prints the content of the current window
- `prompt()` displays a dialogue box that prompts the user for text input
  - Can store response text as a variable
  - Prompts return a string
  - To return a number from a prompt, enter it like this: ``var `[variable name]` = + `[prompt]` ``
  - Converting a string to a number: ``Number(`[number]`)``, ``parseInt(`[number]`)``, or ``parseFloat(`[number]`)``, followed by `Number = num.toString()`
- `resizeBy()` resizes the window by the specified number of pixels
- `resizeTo()` resizes the window to a specified width and height
- `scrollBy()` scrolls the document by a specified number of pixels
- `scrollTo()` scrolls the document to specified coordinates
- `setInterval()` calls a function or evaluates an expression at specified intervals
- `setTimeout()` calls a function or evaluates an expression after a specified interval
- `stop()` stops a window from loading

### Screen Properties

- `availHeight` returns the height of the screen, excluding the windows taskbar
- `availWidth` returns the width of the screen, excluding the windows taskbar
- `colorDepth` returns the bit depth of the color palette for displaying images
- `height` returns total height of the screen
- `pixelDepth` returns color resolution of the screen in bits per pixel
- `width` returns total width of the screen
