# Web Scraping

## General

---

- `robotstxt::paths_allowed()` checks if a web scraping bot is able to access a web page
- Basic rvest functions:
  - `read_html()` reads HTML data from a URL/character string
  - `html_nodes()` selects specified nodes from the HTML document using CSS selectors/tags
  - `html_table()` parses an HTML table into a data frame
  - `html_text()` extracts tag pairs' content
  - `html_name()` extracts tags' names
  - `html_attrs()` extracts all of each tag's attributes
  - `html_attr()` extracts tags' attribute values by name
