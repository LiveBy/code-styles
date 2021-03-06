# Markdown Style Guide

In general:

- Be consistent with the file you found
- Prioritize readability as plaintext over writability or rendered html


## Line length

Hard wrap lines at 80 characters whenever possible. An obvious exception is with
hyperlinks. Move hyperlinks to their own line if they would exceed the 80 char
limit.

Rationale:


## Links

Prefer reference-style links. Always use reference-style links when the same
URL is used multiple times in the file.

Rationale: Reference-style links are more readable than inline links.


## Headings

Prefer hashes for headings over multiple the dashes.

Nesting headings appropriately. Don't jump from h1 to h4 just because you feel
like it.

Headings should always be followed by a single empty line.

Be liberal but consistent with empty lines preceding headings. Two empty lines
is often appropriate before second-level headings (h2).

Rationale: A well-organized Markdown file is a beauty to behold.


## Lists

Prefer single dashes for unordered lists. Don't precede the dash with a space,
and include a single space after the dash.

Good:

```markdown
- one
- two
```

Bad:

```markdown
 * this
 * next
```

Rationale: Single dashes are lighter and easier on the eyes. Starting a list
item with a space is a waste of a character.


### Nested Lists

Nested lists should be indented two spaces.

Good:

```markdown
- level 1
  - level 2
    - level 3
```

Bad:

```markdown
  - level 1
   - level 2
      - level 3
```

Rationale: Two spaces is enough to show hierarchy and looks nice and clean.


### Wrapping List Items

Use hanging indents to align text when list items flow to multiple lines.

Good:

```markdown
- This is a long line that wraps to the next line because it is really long and
  goes to the next line.
- This is a long line that wraps to the next line because it is really long and
  goes to the next line.
```

Bad:

```markdown
- This is a long line that wraps to the next line because it is really long and
goes to the next line.
- This is another long line that wraps to the next line because it is really
   long and goes to the next line.
```

Rationale: Text reads better when multiple lines are aligned.


## Code Blocks

Prefer to use four spaces for [code blocks] if there is only one code format in
the Markdown file. Use fenced code blocks with a language identifier if there
are multiple languages code formats (html, js, css).

Rationale: Indented code blocks are cleaner than fenced code blocks. Labeled
code blocks are messier, but make intent clearer.

Exceptions: One exception to this rule is when you have Markdown examples in a
Markdown file. Use labeled fenced code blocks instead of indented code blocks
in that case.

[Code Blocks]: http://daringfireball.net/projects/markdown/syntax#precode
[Fenced Code Blocks]: https://help.github.com/articles/github-flavored-markdown/#fenced-code-blocks

## Variables and Function names

Use back-ticks when referring to variable or function names inside a paragraph.

TODO: Examples

## Bold / Strong Emphasis

Use double asterisks (`**`) to bold text. Do not use double underscore.

Good:

```markdown
This is **amazing**!
```

Bad:

```markdown
This is __amazing__!
```

Rationale: Double stars conveys strong emphasis better than double underscores.


## Italics / Emphasis

Prefer a single underscore (`_`) to emphasize text over a single asterisk (`*`).

Some Markdown processors have issues when the emphasized content (such as file
names) contain underscores. Feel free to use single asterisks if that is the
case.

Good:

```markdown
This is _pretty_ tasty.
```

OK:

```markdown
This is *pretty_tasty*
```

Bad:

```markdown
This is *pretty* tasty.
```

Rationale: Underscores provide subtler emphasis than asterisks. Additionally,
underlining text is a standard copy editing mark for italicized text, and the
single underscore preceding and following text looks similar to an underline.
