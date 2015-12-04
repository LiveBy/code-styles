# LiveBy HTML Standard Style

Our team strives to write semantic HTML to provide clear and organized markup
for structuring content in web pages.

## [The Living Standard](https://html.spec.whatwg.org/multipage/)

The canonical source for semantic HTML is the HTML specification, a living
document, created by Web Hypertext Application Technology Working Group (WHATWG).

[The HTML specficiation](https://html.spec.whatwg.org/multipage/)

## Specific Formatting Rules

For suggestions on semantic sectioning elements:

![HTML5 sectioning elements flowchart](./assets/html/h5d-sectioning-flowchart.png)

**The following guidelines** are adapted from the [PrimerCSS's HTML Styleguide](http://primercss.io/guidelines/#html)

- Paragraphs of text should always be placed in a ```<p>``` tag. Never use multiple ```<br>``` tags.
- Items in list form should always be in ```<ul>```, ```<ol>```, or ```<dl>```. Never use a set of ```<div>``` or ```<p>```.
- Every form input that has text attached should utilize a <label> tag. Especially radio or checkbox elements.

### Lean markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML. For example:

```html
<!-- Not so great -->
<span class="avatar">
  <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```
