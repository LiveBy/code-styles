# LiveBy JavaScript Standard Style

Our styleguide is based heavily on the JS Standard Style with a few notable departures. Additionally, while the JS Standard Style speaks to many points on coding style, we appended have appended our own ideas of best practice to this document.

[Javascript Standard Style](https://github.com/feross/standard)

## Rules

- **Use 2 spaces** for indentation.

  ```js
  function hello (name) {
    console.log('hi', name)
  }
  ```

- **Use single quotes for strings** except to avoid escaping.

  ```js
  console.log('hello there')
  $("<div class='box'>")
  ```

- **No unused variables.**

  ```js
  function myFunction () {
    var result = something()   // ✗ avoid
  }
  ```

- **Add a space after keywords.**

  ```js
  if (condition) { ... }   // ✓ ok
  if(condition) { ... }    // ✗ avoid
  ```

- **Add a space* before a function declaration's parentheses.

  ```js
  function name (arg) { ... }   // ✓ ok
  function name(arg) { ... }    // ✗ avoid

  run(function () { ... })      // ✓ ok
  run(function() { ... })       // ✗ avoid
  ```

- **Always use** `===` instead of `==`.<br>
  Exception: `obj == null` is allowed to check for `null || undefined`.

  ```js
  if (name === 'John')   // ✓ ok
  if (name == 'John')    // ✗ avoid
  ```

  ```js
  if (name !== 'John')   // ✓ ok
  if (name != 'John')    // ✗ avoid
  ```

- **Infix operators** must be spaced.

  ```js
  // ✓ ok
  var x = 2;
  var message = 'hello, ' + name + '!';
  ```

  ```js
  // ✗ avoid
  var x=2;
  var message = 'hello, '+name+'!';
  ```

- **Commas should have a space** after them.

  ```js
  // ✓ ok
  var list = [1, 2, 3, 4];
  function greet (name, options) { ... }
  ```

  ```js
  // ✗ avoid
  var list = [1,2,3,4];
  function greet (name,options) { ... }
  ```

- **For else statements**, create a new line.

  ```js
  // ✓ ok
  if (condition) {
    // ...
  }
  else {
    // ...
  }
  ```

  ```js
  // ✗ avoid

  if (condition) {
    // ...
  } else {
    // ...
  }
  ```

- **For multi-line if statements,** use curly braces.

  ```js
  // ✓ ok
  if (options.quiet !== true) console.log('done')
  ```

  ```js
  // ✓ ok
  if (options.quiet !== true) {
    console.log('done')
  }
  ```

  ```js
  // ✗ avoid
  if (options.quiet !== true)
    console.log('done')
  ```

- **Always handle the** `err` function parameter.

  ```js
  // ✓ ok
  run(function (err) {
    if (err) throw err
    window.alert('done')
  })
  ```

  ```js
  // ✗ avoid
  run(function (err) {
    window.alert('done')
  })
  ```

- **Always prefix browser globals** with `window.`.<br>
  Exceptions are: `document`, `console` and `navigator`.

  ```js
  window.alert('hi')   // ✓ ok
  ```

- **Multiple blank lines not allowed.**

  ```js
  // ✓ ok
  var value = 'hello world'
  console.log(value)
  ```

  ```js
  // ✗ avoid
  var value = 'hello world'


  console.log(value)
  ```

- **For the ternary operator** in a multi-line setting, place `?` and `:` on their own lines.

  ```js
  // ✓ ok
  var location = env.development ? 'localhost' : 'www.api.com'

  // ✓ ok
  var location = env.development
    ? 'localhost'
    : 'www.api.com'

  // ✗ avoid
  var location = env.development ?
    'localhost' :
    'www.api.com'
  ```

- **For var declarations,** write each declaration in its own statement.

  ```js
  // ✓ ok
  var silent = true
  var verbose = true

  // ✗ avoid
  var silent = true, verbose = true

  // ✗ avoid
  var silent = true,
      verbose = true
  ```

- **Wrap conditional assignments** with additional parentheses. This makes it clear that the expression is intentionally an assignment (`=`) rather than a typo for equality (`===`).

  ```js
  // ✓ ok
  while ((m = text.match(expr))) {
    // ...
  }

  // ✗ avoid
  while (m = text.match(expr)) {
    // ...
  }
  ```
*
## Semicolons

- No semicolons. (see: [1](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding), [2](http://inimino.org/%7Einimino/blog/javascript_semicolons), [3](https://www.youtube.com/watch?v=gsfbh17Ax9I))

  ```js
  window.alert('hi')   // ✓ ok
  window.alert('hi');  // ✗ avoid
  ```

- Never start a line with `(` or `[`. This is the only gotcha with omitting semicolons.

  ```js
  ;(function () {
    window.alert('ok')
  }())
  ```

## Helpful reading

- [An Open Letter to JavaScript Leaders Regarding Semicolons][1]
- [JavaScript Semicolon Insertion – Everything you need to know][2]

##### And a helpful video:

- [Are Semicolons Necessary in JavaScript? - YouTube][3]

All popular code minifiers in use today use AST-based minification, so they can
handle semicolon-less JavaScript with no issues (since semicolons are not required
in JavaScript).

In general, `\n` ends a statement unless:
  1. The statement has an unclosed paren, array literal, or object literal or ends in some
     other way that is not a valid way to end a statement. (For instance, ending with `.`
     or `,`.)
  2. The line is `--` or `++` (in which case it will decrement/increment the next token.)
  3. It is a `for()`, `while()`, `do`, `if()`, or `else`, and there is no `{`
  4. The next line starts with `[`, `(`, `+`, `*`, `/`, `-`, `,`, `.`, or some other
     binary operator that can only be found between two tokens in a single expression.

The first is pretty obvious. Even JSLint is ok with `\n` chars in JSON and parenthesized constructs, and with `var` statements that span multiple lines ending in `,`.

The second is super weird. I’ve never seen a case (outside of these sorts of conversations) where you’d want to do write `i\n++\nj`, but, point of fact, that’s parsed as `i; ++j`, not `i++; j`.

The third is well understood, if generally despised. `if (x)\ny()` is equivalent to `if (x) { y() }`. The construct doesn’t end until it reaches either a block, or a statement.

`;` is a valid JavaScript statement, so `if(x);` is equivalent to `if(x){}` or, “If x, do nothing.” This is more commonly applied to loops where the loop check also is the update function. Unusual, but not unheard of.

The fourth is generally the fud-inducing “oh noes, you need semicolons!” case. But, as it turns out, it’s quite easy to *prefix* those lines with semicolons if you don’t mean them to be continuations of the previous line. For example, instead of this:

```js
foo();
[1,2,3].forEach(bar);
```

you could do this:

```js
foo()
;[1,2,3].forEach(bar)
```

The advantage is that the prefixes are easier to notice, once you are accustomed to never seeing lines starting with `(` or `[` without semis.

*End quote from "An Open Letter to JavaScript Leaders Regarding Semicolons".*

## Tips

### Avoid clever short-hands

Clever short-hands are discouraged, in favor of clear and readable expressions, whenever
possible. So, while this is allowed:

```js
;[1, 2, 3].forEach(bar)
```

This is much preferred:

```js
var nums = [1, 2, 3]
nums.forEach(bar)
```

[1]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[2]: http://inimino.org/~inimino/blog/javascript_semicolons
[3]: https://www.youtube.com/watch?v=gsfbh17Ax9I