# CSS


## Coding Style

- Use a two space indent.
- Put spaces after : in property declarations.
- Do not put a space before : in property declarations
- Put spaces before { in rule declarations.
- Separate selector and property declarations with a new line
- Separate rules with a new line
- End all properties declarations with a ;
- Alphabetize properties within rule declarations
- Properties with values of 0 should *not* have units
- Use lowercase hex color codes `#fff` unless using rgba.
- Do not put spaces inside parentheses for rgb/rgba, transform functions, or media queries (`rgb(10, 100, 200)`)
- Do put a space after the comma in function properties.
- Use /* */ for block comments (instead of multiple //).
- Use // for single-line comments.
- Use a maximum line length of 80 characters (rationale: looking at files side-by-side)
- Use dashes in selectors instead of underscores (.my-class, not .my_class)
- Do not use ids
- Choose semantic class names based on hierarchy and content, not on positioning or visual appearance. (Example: `.site__meta-info`, instead of `.site-menu-small` or `.site-top-section`).


## CSS/Sass Coding Guidelines

Every stylesheet should be easy to read, scan, add to, and collaborate on. Our current system and nomenclature builds on top of _components_, where CSS files live alongside the component they are styling: `component/style.scss`. These files are all imported via `stylesheets/_components.scss`.

This is an example of a declaration:

`.component__element.is-modifier {}`

Two important considerations:

* The `component` fragment matches the folder name of the React component it's providing styles to.
* The `.is-modifier` class should never be written on its own outside of the component class. This avoids naming collisions and provides a consistent use of modifiers.
* We don't use `#ids` for style purposes.

#### Example

Take a component called `site/index.jsx` that renders a site item on the picker. Imagine we are going to set the color for the site title to #333 and change it to #444 when the site is a Jetpack site. Our Sass file will sit alongside `site/index.jsx` and be called `site/style.scss`. Its content will be written like:

**Good**

```scss
.site__title {
    color: #333;

    &.is-jetpack {
        color: #444;
    }
}
```

**Bad**
```scss
.site {
    .title {
        color: #333;

        .jetpack {
            color: #444;
        }
    }
}
```

The modifier classes are always attached to a base element (the wrapper of a component). Since every element will have a direct class to be selected with, we avoid descendant selectors and child selectors. We also avoid indenting selectors in Sass files in favor of single selectors. The main exceptions are precisely the `is-modifier` class, and the cases where the context needs to change a given component's accidents.

```scss
// Modify 'site__title' for in CurrentSite component's display
.current-site .site__title {
    color: #444;
}
```

The expressiveness of the selector above clearly conveys that there are two separate components involved (CurrentSite and Site). We also keep CSS specificity in check. Avoid using Sass indents for simple selectors — they obfuscate the cascade.

It's important to note that we don't reuse classes, we reuse components.

## Components

These practices mean that a component will work anywhere it is included by default, and that the developer won't need to go hunting for the relevant CSS. Any modifications will happen in the context/parents, and will be minimal in nature. Where and how changes will affect the rendering of the app will thus be clearer. (If you edit the button-component's Sass file you know you are editing it for everyone.)

## General Syntax and Writing Rules

Apart from the above structure, please adhere to these guidelines:

- Follow the [WordPress CSS Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/css/), unless it contradicts something stated in this document.
- Avoid `#` selectors for style purposes. Their specificity becomes troublesome to manage fairly quickly.
- Don't use the `!important` declaration. If you think you need to do it, consider fixing the root cause.
- Avoid using universal selectors (`*`).
- Use hyphens, not underscores or camelCase, when naming things like IDs, classes, variable names, mixins, placeholders. Good: `.site-title`, Bad: `.siteTitle` or `.site_title`.
- The only exception is the `__` syntax to signal the relationship within a component.
- Avoid using over-qualified selectors like `div.my-class`.

## Classes

Classes are the fundamental building block of our stylesheets. Using them appropriately and consistently is important to keep a maintainable and enjoyable codebase.

- Generic class names are deemphasized in favor of component-based structures. Instead of defining generic classes in a shared stylesheet, we construct components that come with both markup and styles ready to be used.
- Avoid redundant bits of information that are provided by the HTML element or other contexts. (Don't do `.site__content-box` on a `div`, the `box` is not necessary.)
- We keep one level of prefix for single components present in the class name: `.site__title` instead of `.site .title`. This may seem verbose but it provides more flexibility, clear direct selectors, and immediate recognizability of its role in a large codebase like Calypso. Classes are not just for style purposes, they should provide meaning to the reader parsing the document.
- Keep class names lean and to the point. Name classes the same way you would describe what the content of an element is to a stranger.


### Adding a new Sass file

`assets/stylesheets/style.scss` is the root stylesheet for the application. Site-wide styles should be placed in `assets/stylesheets/`, and `style.scss` will need to be updated with a reference to the new file.

Styles for React components should live in the same directory as the component's `.jsx` file.

### Imports

- Declare all of your `@import` dependencies at the top of a file that needs it/them.
- Don't `@import` dependencies in a global file and just hope it filters down to your partial.

### Nesting

### Sass

- Do not nest selectors in general. Exceptions are `:hover`/`:focus`/`::before`/`.is-modifier`, and alike.
- Keep nesting to 2 levels deep at most.
- List items inside a selector in the following order (not all will necessarily be present):
    1. `@extend`(s).
    2. alphabetical property list for the element.
    3. mixin(s).
    4. nested selectors, with a space above each to keep them visually distinct.

Example of the above:

```scss
.parent {
    @extend %awesomeness;
    border: 1px solid;
    z-index: 5;
    @include moar-awesome( true );

    &::before {
        // and so on
    }
}
```

### Mixins vs Extends

- Use `@extend` when in doubt, using the `%placeholder` syntax. This will produce leaner output.
- Don't use mixins for anything that doesn't accept an argument. This is `@extend` territory.
* DO read [this article](http://miguelcamba.com/blog/2013/07/11/sass-placeholders-versus-mixins-and-extends/) if you don't understand `@extend`.
