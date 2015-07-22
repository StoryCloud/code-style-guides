# HTML Style Guide

The following document outlines a style guide for HTML pages and templates.

# Tags

- Always include a trailing slash in self-closing elements (e.g. `<br/>`, not `<br>`).
- Don't omit optional closing tags (e.g. `</li>` or `</body>`).

# Quotes

- Use double quotes.
- Don't omit quotes.

# Whitespace

- 4 spaces for indentation.
- Strip trailing whitespace.

# Attributes

HTML attributes can be indented 4 spaces OR aligned.

4-space indentation:

```html
<marquee
    behavior="alternate"
    bgcolor="yellow"
    scrollamount="15">
    Hello World!
</marquee>
```

Aligned:

```html
<div href="http://www.example.com/"
     class="link">
    Link Text
</a>
```

# Identification

- Prefer `class` for identifying elements that need to be selected for styling
  or queried via JavaScript.

# Reducing markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many
times this requires iteration and refactoring, but produces less HTML. Take the
following example:

```html
<!-- Not so great -->
<span class="avatar">
    <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```

# Trivialities

## Doctype

```html
<!DOCTYPE html>
<html>
...
</html>
```

## lang

The HTML `lang` attribute should be included and its value should conform to
[W3C standards](http://www.w3.org/TR/html401/struct/dirlang.html) and
[RFC 1766](http://www.ietf.org/rfc/rfc1766.txt).

## IE compatibility mode is deprecated

The IE Document Mode selector (`<meta http-equiv="X-UA-Compatible"
content="IE=edge" />`) is now deprecated and should not be used
[(Source)](http://msdn.microsoft.com/en-us/library/ie/dn384051(v=vs.85).aspx). Per
Microsoft's recommendation, use the IE11 Standards selector, `<!DOCTYPE html>`
instead.

## Character encoding

```html
<head>
    <meta charset="utf-8">
</head>
```
