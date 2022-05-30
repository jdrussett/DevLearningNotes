<!---

Markdown syntax reference: https://www.markdownguide.org/basic-syntax/

-->

# Heading 1 (largest)

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6 (smallest)

Paragraph one. Separate from the next paragraph with more than one space.

Paragraph two.

Inserting line break - ending this line with two or more spaces.  
New line.

**Bolded text**  
*Italicized text*  
***Bolded and italicized text***

Block quote exhibited below:
> block quote

Nested block quote exhibited below:
> outer block quote
>> inner block quote
> continuing the outer block quote

Paragraphing with block quotes:
> First paragraph of blockquotes
>
> Second paragraph of blockquotes

[a comment that will not appear in the document]: #

`inline code`

Referencing a code command inside a code phrase: ``code chunk `this is the command` more code chunk``

Ordered List:

1. ordered list first item
2. ordered list second item
   1. ordered list second item first sub-item
   2. ordered list second item second sub-item
3. ordered list third item

Unordered List:

- unordered list first item
- unordered list second item
  - unordered list sub-item
- unordered list third item
   1. include an ordered list within an unordered list
   2. another item in the ordered list within an unordered list
- 1967\. release year of Sgt. Pepper's Lonely Heart's club band (start an unordered list item with a number & period)

    indenting this text to serve as a paragraph in between items on the list

- continuing the list now...

    > putting a block quote in the middle of the list

- more items on the list
- last item of the list

Create a code block by indenting:

    List<String> stringList = new List<String>{'hi', 'hello', 'how are you'};
    System.debug(stringList);

Create a horizontal rule with three dashes:

---

Add an in-line hyperlink: [Google.com](https://www.google.com)

Include an image in markdown:

![This is alternative text to the image if doesn't load...? maybe](/Resources/Image%20Resources/Git_Notes_image1.png "Optional title of included image file")
