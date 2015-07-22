# CSS Style Guide

The following document outlines a style guide for CSS and Sass stylesheets.

# Whitespace

- Use 4 spaces for indentation.
- Strip trailing whitespace.
- Use empty lines to separate rules.

```scss
// Getting scrunched here.
.selector {
    width: 100px;
}
.selector {
    width: 200px;
}


// More room to breathe.

.selector {
    width: 100px;
}

.selector {
    width: 200px;
}
```

# Comments

Describe components, how they work, their limitations, and the way they are
constructed. Don't leave others in the team guessing as to the purpose of
uncommon or non-obvious code.

- Place comments on a new line above their subject.
- Keep line-length to a sensible maximum, e.g., 80 columns.
- Make liberal use of comments to break CSS code into discrete sections.
- Use "sentence case" comments and consistent text indentation.
- Separate the start the comment from the words with a single place.

```scss
//i'm just chillin' here (Bad.)

// This is a properly-punctuated sentence. (Good.)
```

Example:

```scss
/*
 * The first sentence of the long description starts here and continues on this
 * line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 */

// Basic comment.
```

# Format

- Use one discrete selector per line in multi-selector rulesets.
- Include a single space before the opening brace of a ruleset.
- Include one declaration per line in a declaration block.
- Use one level of indentation for each declaration.
- Include a single space after the colon of a declaration.
- Use lowercase and shorthand hex values, e.g., `#aaa`. No `color: red`.
- Use double quotes. e.g., `content: ""`.
- Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
- *Where allowed*, avoid specifying units for zero-values, e.g., `margin: 0`.
- Include a space after each comma in comma-separated property or function values.
- Include a semi-colon at the end of the last declaration in a declaration block.
- Place the closing brace of a ruleset in the same column as the first character
  of the ruleset.
- Separate each ruleset by a blank line.

```scss
.selector-1,
.selector-2,
.selector-3[type="text"] {
    box-sizing: border-box;
    display: block;
    font-family: helvetica, arial, sans-serif;
    color: #333;
    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
}

.selector-a,
.selector-b {
    padding: 10px;
}
```

## Declaration order

- Cluster related properties (e.g. positioning and box-model) together.

```scss
.selector {
    // Positioning
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    // Display & Box Model
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;

    // Other
    background: #000;
    color: #fff;
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;
}
```

## Exceptions and slight deviations

Long, comma-separated property values - such as collections of gradients or
shadows - can be arranged across multiple lines in an effort to improve
readability and produce more useful diffs.

```scss
.selector {
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```

## Preprocessors

The following guidelines are in reference to Sass.

- Limit nesting to 1 level deep. Reassess any nesting more than 2 levels
  deep. This prevents overly-specific CSS selectors.
- Avoid large numbers of nested rules. Break them up when readability starts to
  be affected. Preference to avoid nesting that spreads over more than 20 lines.
- Always place `@extend` statements on the first lines of a declaration block.
- Where possible, group `@include` statements at the top of a declaration block,
  after any `@extend` statements.
- Consider prefixing custom functions with `sc-`. This helps to avoid any
  potential to confuse your function with a native CSS function, or to clash
  with functions from libraries.

```scss
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: x-grid-unit(1);
}
```

# Practical example

An example of various conventions.

```scss
/*
 * Column layout with horizontal scroll.
 *
 * This creates a single row of full-height, non-wrapping columns that can
 * be browsed horizontally within their parent.
 *
 * Example HTML:
 *
 * <div class="grid">
 *     <div class="cell cell-3"></div>
 *     <div class="cell cell-3"></div>
 *     <div class="cell cell-3"></div>
 * </div>
 */

/*
 * Grid container
 *
 * Must only contain `.cell` children.
 *
 * 1. Remove inter-cell whitespace
 * 2. Prevent inline-block cells wrapping
 */

.grid {
    height: 100%;
    font-size: 0; // 1
    white-space: nowrap; // 2
}

/*
 * Grid cells
 *
 * No explicit width by default. Extend with `.cell-n` classes.
 *
 * 1. Set the inter-cell spacing
 * 2. Reset white-space inherited from `.grid`
 * 3. Reset font-size inherited from `.grid`
 */

.cell {
    position: relative;
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    height: 100%;
    padding: 0 10px; // 1
    border: 2px solid #333;
    vertical-align: top;
    white-space: normal; // 2
    font-size: 16px; // 3
}

// Cell states

.cell-is-animating {
    background-color: #fffdec;
}

// Cell dimensions

.cell-1 {
    width: 10%;
}
.cell-2 {
    width: 20%;
}
.cell-3 {
    width: 30%;
}
.cell-4 {
    width: 40%;
}
.cell-5 {
    width: 50%;
}

// Cell modifiers

.cell-detail,
.cell-important {
    border-width: 4px;
}
~~~~

# License

*Principles of writing consistent, idiomatic CSS* by Nicolas Gallagher is licensed under the [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/).

Based on a work at [github.com/necolas/idiomatic-css](https://github.com/necolas/idiomatic-css).
