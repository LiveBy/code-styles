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
URL is used in multiple files.

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

Prefer single dashes for lists. Don't precede the dash with a space.

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

### Wrapping text in lists

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

Rationale: Text flows better when multiple lines are aligned.

## Code Blocks

Prefer to use four spaces for code blocks if there is only one code format in
the Markdown file. Use labeled fenced code blocks if there are multiple
different code formats (html, js, css).

Rationale: Indented code blocks are cleaner than fenced code blocks. Labeled
code blocks are messier, but make intent clearer.

## Variables and Function names

Use back-ticks when referring to variable or function names inside a paragraph.
