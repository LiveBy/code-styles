# LiveBy JavaScript Standard Style

Our styleguide is a weave based on JS Standard Style and Automattic's Calypso project.

[Javascript Standard Style](https://github.com/feross/standard)
[Calypso JS Style-Guide](https://github.com/Automattic/wp-calypso/blob/master/docs/coding-guidelines/javascript.md)

## Naming Conventions

Variable and function names should be full words, using camel case with a lowercase first letter. This also applies to abbreviations and acronyms.

```js
// Good
var userIdToDelete, siteUrl;

// Bad
var userIDToDelete, siteURL;
```

Constructors intended for use with new should have a capital first letter (UpperCamelCase).

Names should be descriptive, but not excessively so. Exceptions are allowed for iterators, such as the use of `i` to represent the index in a loop.

## Comments

Comments come before the code to which they refer, and should always be preceded by a blank line unless inserted as the first line in a block statement. Capitalize the first letter of the comment, and include a period at the end when writing full sentences. There must be a single space between the comment token (//) and the comment text.

Single line comments:

```js
someStatement();

// Explanation of something complex on the next line
$( 'p' ).doSomething();
```

When adding documentation, use the [jsdoc](http://usejsdoc.org/) format.

```js
/**
 * Represents a book.
 * @constructor
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 */
function Book(title, author) {

}

```

Multi-line comments that are not a jsdoc comment should use `//`:

```js
//
// This is a comment that is long enough to warrant being stretched
// over the span of multiple lines.
```

Inline comments are allowed as an exception when used to annotate special arguments in formal parameter lists:

```js
function foo( types, selector, data, fn, /* INTERNAL */ one ) {
    // Do stuff
}
```
## Type Checks

These are the preferred ways of checking the type of an object:

- String: `typeof object === 'string'`
- Number: `typeof object === 'number'`
- Boolean: `typeof object === 'boolean'`
- Object: `typeof object === 'object'`
- null: `object === null`
- undefined: `object === undefined` or for globals `typeof window.someGlobal === 'undefined'`

However, you don't generally have to know the type of an object. Prefer testing
the object's existence and shape over its type.

## Existence and Shape Checks

Prefer using the [power](http://www.ecma-international.org/ecma-262/5.1/#sec-9.2)
of "truthy" in JavaScript boolean expressions to validate the existence and shape
of an object to using `typeof`.

The following are all false in boolean expressions:

- `null`
- `undefined`
- `''` the empty string
- `0` the number

But be careful, because these are all true:

- `'0'` the string
- `[]` the empty array
- `{}` the empty object
- `-1` the number


To test the existence of an object (including arrays):
```js
if ( object ) { ... }
```

To test if a property exists on an object, regardless of value, including `undefined`:
```js
if ( 'desired' in object ) { ... }
```

To test if a property is present and has a truthy value:
```js
if ( object.desired ) { ... }
```

To test if an object exists and has a property:
```js
if ( object && 'desired' in object ) { ... }
if ( object && object.desired ) { ... }
```



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

- **Keep else statements** on the same line as their curly braces.

  ```js
  // ✓ ok
  if (condition) {
    // ...
  } else {
    // ...
  }
  ```

  ```js
  // ✗ avoid
  if (condition) {
    // ...
  }
  else {
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

### Semicolon - Helpful reading

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

### Semicolon - Tips

#### Avoid clever short-hands

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

## Additional Best Practices

### Iteration

The functional programming inspired methods that were added in ECMA5 improve readability. Use them throughout.

```js
var posts = postList.map( function( post ) {
	return <Post post={ post } key={ post.global_ID } />;
} );
```

When iterating over a large collection using a for loop, it is recommended to store the loop’s max value as a variable rather than re-computing the maximum every time:


### Objects

Object declarations can be made on a single line if they are short (remember the line length guidelines). When an object declaration is too long to fit on one line, there must be one property per line. Property names only need to be quoted if they are reserved words or contain special characters:

```js
// Preferred
var map = {
    ready: 9,
    when: 4,
    'you are': 15
};

// Acceptable for small objects
var map = { ready: 9, when: 4, 'you are': 15 };

// Bad
var map = { ready: 9,
    when: 4, 'you are': 15 };

```

### Arrays and Function Calls

Always include extra spaces around elements and arguments:

```js
array = [ a, b ];

foo( arg );

foo( 'string', object );

foo( options, object[ property ] );

foo( node, 'property', 2 );
```

## Best Practices

### Variable names

The first word of a variable name should be a noun or adjective (not a verb) to avoid confusion with functions.

You can prefix a variable with verb only for boolean values when it makes code easier to read.

```js
// bad
const play = false;

// good
const name = 'John';
const blueCar = new Car( 'blue' );
const shouldFlop = true;
```

### Function names

The first word of a function name should be a verb (not a noun) to avoid confusion with variables.

```js
// bad
function name() {
    return 'John';
}

// good
function getName() {
    return 'John';
}

// good
function isValid() {
    return true;
}
```

### Arrays

Creating arrays in JavaScript should be done using the shorthand [] constructor rather than the new Array() notation.

```js
var myArray = [];
```

You can initialize an array during construction:

```js
var myArray = [ 1, 'WordPress', 2, 'Blog' ];
```

In JavaScript, associative arrays are defined as objects.

### Objects

There are many ways to create objects in JavaScript. Object literal notation, `{}`, is both the most performant, and also the easiest to read.

```js
var myObj = {};
```

Object literal notation should be used unless the object requires a specific prototype, in which case the object should be created by calling a constructor function with new.

```js
var myObj = new ConstructorMethod();
```

Object properties should be accessed via dot notation, unless the key is a variable, a reserved word, or a string that would not be a valid identifier:

```js
prop = object.propertyName;
prop = object[ variableKey ];
prop = object['default'];
prop = object['key-with-hyphens'];
```

## ES6

We support and encourage ES6 features thanks to [Babel](https://babeljs.io/) transpilation and the accompanying polyfill. There are still a couple of minor caveats to be aware of [regarding Classes](https://babeljs.io/docs/advanced/caveats/).

### Let and Const

You can use `const` for all of your references.

> Why? This ensures that you can't reassign your references (mutation), which can lead to bugs and difficult to comprehend code.

```javascript
// good
var a = 1,
    b = 2;

// better
const a = 1,
    b = 2;
```

If you must mutate references, you can use `let`. Otherwise `const` is preferred.

> Why? `let` is block-scoped rather than function-scoped like `var`.

```javascript
// good
var count = 1;
if ( true ) {
    count += 1;
}

// better
let count = 1;
if ( true ) {
    count += 1;
}
```

Note that both `let` and `const` are block-scoped.

```javascript
// const and let only exist in the blocks they are defined in.
{
    let a = 1;
    const b = 1;
}
console.log( a ); // ReferenceError
console.log( b ); // ReferenceError
```

More about:

- [Let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) at MDN
- [Const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) at MDN

### Arrow Functions

When you must use function expressions (as when passing an anonymous function), you can use arrow function notation.

> Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

> Why not? If you have a fairly complicated function, you might move that logic out into its own function declaration.

```javascript
// good
function Person() {
    this.age = 0;

    setInterval( function() {
        this.age++;
    }.bind( this ), 1000 );
}
let p = new Person();

// better
function Person() {
    this.age = 0;

    setInterval( () => {
        this.age++;
    }, 1000 );
}
let p = new Person();
```

If the function body fits on one line and there is only a single argument, feel free to omit the braces and parentheses, and use the implicit return. Otherwise, add the parentheses, braces, and use a `return` statement.

> Why? Syntactic sugar. It reads well when multiple functions are chained together.

> Why not? If you plan on returning an object.

```javascript
// bad
// it's too magic, it works only with parentheses, otherwise it returns collection of undefine values
[ 1, 2, 3 ].map( x => ( { value: x * x } ) );

// good
[ 1, 2, 3 ].map( x => x * x );

// good
[ 1, 2, 3 ].reduce( ( total, n ) => {
    return total + n;
}, 0 );

```

More about:

- [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) at MDN

### Object Property Shorthand

You can use property value shorthand.

> Why? It is shorter to write and descriptive.

```javascript
const lukeSkywalker = 'Luke Skywalker';

// good
const obj = {
    lukeSkywalker: lukeSkywalker,
};

// better
const obj = {
    lukeSkywalker,
};
```

Group your shorthand properties at the beginning of your object declaration.

> Why? It's easier to tell which properties are using the shorthand.

```javascript
const anakinSkywalker = 'Anakin Skywalker',
    lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    lukeSkywalker,
    episodeThree: 3,
    mayTheFourth: 4,
    anakinSkywalker,
};

// good
const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
};
```

More about:

- [Object Property Shorthand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Property_definitions) at MDN

### Object Method Shorthand

You can use object method shorthand.

```javascript
// good
const atom = {
    value: 1,

    addValue: function ( value ) {
        return atom.value + value;
    },
};

// better
const atom = {
    value: 1,

    addValue( value ) {
        return atom.value + value;
    },
};
```

More about:

- [Object Method Shorthand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Method_definitions) at MDN

### Object Computed Properties

You can use computed property names when creating objects with dynamic property names.

> Why? They allow you to define all the properties of an object in one place.

```javascript

function getKey( k ) {
    return `a key named ${k}`;
}

// good
const obj = {
    id: 5,
    name: 'San Francisco',
};
obj[ getKey( 'enabled' ) ] = true;

// better
const obj = {
    id: 5,
    name: 'San Francisco',
    [ getKey( 'enabled' ) ]: true,
};
```

More about:

- [Object Computed Properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names) at MDN

### Template Strings

When programmatically building up strings, you can use template strings instead of concatenation.

> Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

```javascript
// good
function sayHi( name ) {
    return 'How are you, ' + name + '?';
}

// better
function sayHi( name ) {
    return `How are you, ${ name }?`;
}
```

More about:

- [Template Strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings) at MDN

### Destructuring

You can use object destructuring when accessing and using multiple properties of an object.

> Why? Destructuring saves you from creating temporary references for those properties.

```javascript
// good
function getFullName( user ) {
    const firstName = user.firstName,
        lastName = user.lastName;

    return `${ firstName } ${ lastName }`;
}

// better
function getFullName( user ) {
    const { firstName, lastName } = user;

    return `${ firstName } ${ lastName }`;
}

// best
function getFullName( { firstName, lastName } ) {
    return `${ firstName } ${ lastName }`;
}
```

You can use array destructuring.

```javascript
const arr = [ 1, 2, 3, 4 ];

// good
const first = arr[0],
    second = arr[1];

// better
const [ first, second ] = arr;
```

Use object destructuring for multiple return values, not array destructuring.

> Why? You can add new properties over time or change the order of things without breaking call sites.

```javascriptts only the data they need
function processInput( input ) {
    let left, right, top, bottom;
    // some assignment happens
    return { left, right, top, bottom };
}
const { left, top } = processInput( input );
```

More about:

- [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) at MDN

### Default Parameters

You can use default parameter syntax rather than mutating function arguments.

```javascript
// really bad
function handleThings( opts ) {
    // No! We shouldn't mutate function arguments.
    // Double bad: if opts is falsy it'll be set to an object which may
    // be what you want but it can introduce subtle bugs.
    opts = opts || {};
    // ...
}

// good
function handleThings( opts ) {
    if ( opts === void 0 ) {
        opts = {};
    }
    // ...
}

// better
function handleThings( opts = {} ) {
    // ...
}
```

More about:

- [Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) at MDN

### Rest

Never use `arguments`, opt to use rest syntax `...` instead.

> Why? `...` is explicit about which arguments you want pulled. Plus rest arguments are a real Array and not Array-like like `arguments`.

```javascript
// bad
function concatenateAll() {
    const args = Array.prototype.slice.call( arguments );

    return args.join( '' );
}

// good
function concatenateAll( ...args ) {
    return args.join( '' );
}
```

More about:

- [Rest](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) at MDN

### Array Spreads

You can use array spreads `...` to copy arrays.

```javascript
// good
const itemsCopy = items.slice();

// better
const itemsCopy = [ ...items ];
```

More about:

- [Array Spreads](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator) at MDN
