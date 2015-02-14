# JavaScript Style Guide

The following document outlines a style guide for JavaScript programs.

# Prelude

StoryCloud's JavaScript Style Guide extends Douglas Crockford's
[Code Conventions for the JavaScript Programming Language](http://javascript.crockford.com/code.html). Everything
in that style guide also applies to this style guide. Please familiarize
yourself with it.

## Common Courtesy

- Use ECMAScript 5.
  - We don't support ECMAScript 3-only browsers, so constructs like `typeof
    variable === 'undefined'` can be replaced with `variable === undefined`, et
    al.
  - ECMAScript 6 is not yet standardized. While many browsers and runtimes have
    already implemented some proposed features, it would be unwise to use them,
    because their behavior could change. Platform portability, compatibility
    with existing tools, incomplete implementation, and lack of thorough
    analysis of the value or harm of new features are also concerns.
- Place `'use strict';` at the top of functions.
- Don't be tricky.

# Formatting

- Strip trailing whitespace.
- Use Unix linefeeds (LF).
- End files with a newline.

Most text editors can be configured to format whitespace. Please do this to
avoid whitespace-oriented commits and diffs.

Use JSCS to validate the format of your code. Your editor may offer JSCS
integration, which you may find useful if you are not familiar with the style
guide. You can also use our projects' Grunt interface.

# Grammar

## Use real words for identifiers.

"element" is best written as "element", not "el", "elm", "elem", or "e".

Ubiquitous acronyms such as "http" and "url" are permissible.

## Capitalize only the first letter of words in identifiers.

A phrase such as "File Transfer URI", which contains a normally-capitalized
acronym, has the identifier `fileTransferUri` (as opposed to something like
`fileTransferURI`).

# Syntax

## Functions

Use [function expressions][]. Do not use [function declarations][].

[function expressions]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function
[function declarations]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function

Do:

```js
var procedure = function () {
    // Function body...
};
```

Don't:

```js
function procedure() {
    // Function body...
}
```

Function expressions are more versatile than function declarations. Also, when
written alongside immediately-invoked function expressions which return
functions, the form is more consistent:

```js
var procedure0 = function () {
        // Function body...
    },
    procedure1 = (function () {
        return function () {
            // Function body...
        };
    }());
```

Like `var` statements, function declarations also "hoist" a variable in the
enclosing function's scope, which can result in errors not obvious to the
talented, casual observer. Just as we define all variables at the top of a
function to clarify their scope (and as declared functions *also* define
variables), we also define all nested functions at the top of the function.

## Strings

Use single quotes (`'`) for string literals.

Use string concatenation. Do not use "multiline strings".

Do:

```js
var a = 'The quick brown fox ' +
        'jumps over the lazy dog';
```

Don't:

```js
var a = 'The quick brown fox \
jumps over the lazy dog.'
```

Multiline strings are harmful because a trailing space following the escaping
`\` will result in a syntax error invisible to the human eye.

# Quality

Use JSHint to validate the quality of your code and check for errors.

It is highly recommended that you integrate JSHint into your editor, or switch
to an editor that offers integration. Real-time error reporting can make you
more productive by pointing out syntactic and logical errors before runtime.

# Style

## Leverage the functional programming paradigm.

Prefer `forEach`, `map`, `filter` and `reduce` from `Array.prototype` over `for` loops.

Prefer `every` and `some` from `Array.prototype` over `continue` and `break`.

Prefer `Object.keys(object).forEach` over `for in` loops.

Because tail calls are not yet widely implemented, use `while` and `do` for
algorithms that might grow the call stack boundlessly.

Aggregate operations provide forms for iterating over collections that are more
precise and oftentimes more useful than their procedural alternatives.

# Credits

Influenced by:

- [Maintainable JavaScript](http://youtu.be/3MejbqcMC08)
- [Programming Style and Your Brain](http://youtu.be/_EANG8ZZbRs)
- [JavaScript - The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)
