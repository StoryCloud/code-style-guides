# JavaScript Style Guide

The following document outlines a style guide for JavaScript programs.

## General principles

- Prefer ECMAScript 5.
  - We don't support ECMAScript 3-only browsers, so constructs like `typeof
    variable === 'undefined'` can be replaced with `variable === undefined`, et
    al.
  - Open-source code should use ECMAScript 5, as distributed programs should not
    require flags.
  - Our Node.js servers utilize some ECMAScript 6 features. Feel free to use
    those features in that environment, if the code is unlikely to be ported
    elsewhere.
- Place `'use strict';` at the top of scripts or functions.
- Don't be tricky.
- Do be explicit.

## Formatting

Configure your text editor to manage the following whitespace rules:

- Strip trailing whitespace.
- Use Unix linefeeds (LF).
- End files with a newline.

This helps to avoid whitespace-oriented commits and diffs. Installing an
[editorconfig plugin][] is one easy way of enabling these rules.

Use JSCS to validate the format of your code. Our formatting rules derive from
[Code Conventions for the JavaScript Programming Language][]. Your editor may
offer JSCS integration, which you may find useful if you are not familiar with
the style guide. You can also use our projects' Grunt or Gulp interfaces.

[Code Conventions for the JavaScript Programming Language]: http://javascript.crockford.com/code.html
[editorconfig plugin]: http://editorconfig.org/#download

## English

### Spelling

Use real words for identifiers.

For instance, "element" is best written as "element", not "el", "elm", "elem",
or "e".

Ubiquitous acronyms such as "http" and "url" are permissible.

### Capitalization

Capitalize only the first letter of words in identifiers.

For instance, a phrase such as "File Transfer URI", which contains a
normally-capitalized acronym, has the identifier `fileTransferUri` (as opposed
to something like `fileTransferURI`).

### Word choice

Prefer descriptiveness, then brevity. Strive for clarity; avoid ambiguity.

Functions are verbs, everything else should be nouns.

## Syntax

### Variables

If ECMAScript 6 features are available, prefer `const`. Use `let` only when the
value needs to change.

`const` and `let` variables should be defined separately, and close to their
site of first use. `var` statements should be placed at the top of a function.

## Quality

Use JSHint to validate the quality of your code and check for errors.

It is highly recommended that you integrate JSHint into your editor, or switch
to an editor that offers integration. Real-time error reporting can make you
more productive by pointing out syntactic and logical errors before runtime.

## Style

### Functionalism

Prefer `forEach`, `map`, `filter` and `reduce` over `for` loops.

Prefer `every` and `some` over `continue` and `break`.

Prefer `Object.keys(object).forEach` or a `forOwn` function over `for in` loops.

Because tail calls are not yet widely implemented, use `while` and `do` for
algorithms that might grow the call stack boundlessly.

Aggregate operations provide forms for iterating over collections that are more
precise and oftentimes more useful than their procedural alternatives.

### Object-orientation

You can leverage object-oriented design patterns such as encapsulation,
composition, and inheritance in JavaScript. Create functions whose instance
variables represent private and protected members. From these functions, return
objects with methods to access and possibly manipulate the instance
variables. Create functions with extended interfaces that mutate instances of
their parents to effect inheritance.

Example:

```js
var makeMammal = function (data) {
    var self = {};
    self.getName = function () {
        return data.name;
    };
    self.says = function () {
        return data.saying === undefined ? '' : data.saying;
    };
    return self;
};

var myMammal = makeMammal({name: 'Herb'});

var makeCat = function (data) {
    var self;
    data.saying = data.saying === undefined ? 'meow' : data.saying;
    self = makeMammal(data);
    self.purr = function (n) {
        var message = '',
            index;
        for (index = 0; index < n; index += 1) {
            if (message.length > 0) {
                message += '-';
            }
            message += 'r';
        }
        return message;
    };
    self.getName = function () {
        return self.says() + ' ' + data.name +
            ' ' + self.says();
    };
    return self;
};

var myCat = makeCat({name: 'Henrietta'});
```

### Existence

In JavaScript, the values `false`, `undefined`, `null` and `NaN` are falsy, but
so are `''` and `0`. This is unfortunate, because sometimes empty strings and
zero are "valid" values from a business perspective. Therefore, when checking
for the "existence" of a value, it is unreliable to rely on truthiness or
falsiness. Instead, you should explicitly check for bottom values.

Do:

```js
var number = value === undefined ? 100 : value;
if (number !== undefined) {
    // ...
}
```

Don't:

```js
var number = value || 100; // Excludes 0.
if (number) {
    // Won't execute if the value is 0.
}
```

### Simplicity

It's possible to do lots of things on one line. But that can make your code
complex and confusing. You should try to do just one thing per line.

Do:

```js
value = array[index];
index += 1;
```

Don't:

```js
value = array[index++];
```

### Abstraction

Abstract away complex or roundabout routines to make your intent obvious.

For instance, some people use the value returned from `indexOf` to test for the
existence of substrings or elements. But it would be better to abstract that
implication into a `contains` function, as you probably care about existence,
not indices.

Do:

```js
if (contains(array, 'value')) {
    // ...
}
if (isInteger(value)) {
    // ...
}
```

Don't:

```js
if (array.indexOf('value') > -1) {
    // ...
}
if (!isNaN(parseInt(value, 10))) {
    // ...
}
```

## Credits

Influenced by:

- [Maintainable JavaScript](http://youtu.be/3MejbqcMC08)
- [Programming Style and Your Brain](http://youtu.be/_EANG8ZZbRs)
- [JavaScript - The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)
