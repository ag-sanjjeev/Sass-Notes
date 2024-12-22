## &#10162; Strings:
Sass can handle and work with strings. Sass has various functionality to deal with string operations.

### &#9780; Overview:
1. [Quoted Strings](#-quoted-strings)
2. [Unquoted Strings](#-unquoted-strings)
3. [Strings Concatenation](#-strings-concatenation)
4. [String Manipulation](#-string-manipulation)

### &#10022; Quoted Strings:
It is a sequence of characters, which is enclosed with single or double quotes. It represent textual data within Sass.

```scss
$my-string: "value";
```

### &#10022; Unquoted Strings:
It is a sequence of characters, which are used for identifiers, property names and values. It can be used often in conjunction with interpolation.

```scss
$font-family: sans-serif;
```

### &#10022; Strings Concatenation:
Strings can be concatenated with or without the plus symbol operator `+`. 

*With operator:*

```scss
$border-width: 1px;
$border-style: solid;
$border-color: red;

.card.#{$border-style + "." + $border-color} {
  border-style: $border-style;
  border-width: $border-width;
  border-color: $border-color;
}
```

*Respective CSS Output:*

```css
.card.solid.red {
  border-style: solid;
  border-width: 1px;
  border-color: red;
}
```

*Without operator:*

```scss
$border-width: 1px;
$border-style: solid;
$border-color: red;

.card {
  border: $border-width $border-style $border-color;
}
```

*Respective CSS Output:*

```css
.card {
  border: 1px solid red;
}
```

### &#10022; String Manipulation:
Sass provides various functions related to strings manipulation:

- `str-index()`: Returns the index of a substring within a string.
- `str-insert()`: Inserts a string at a specific index.
- `str-length()`: Returns the length of a string.
- `str-slice()`: Extracts a substring from a string.
- `to-lower-case()`: Converts a string to lowercase.
- `to-upper-case()`: Converts a string to uppercase.
- `unquote()`: Removes quotes from a string.
- `quote()`: Adds quotes to a string.

```scss
$font: "600 14px sans-serif";

$font-weight: str-slice($font, 1, 3);
$font-size: str-slice($font, 5, 9);
$font-family: str-slice($font, 10, str-length($font));

@debug $font-weight;
@debug $font-size;
@debug $font-family;
@debug str-index($font, "14px");
@debug to-upper-case($font-family);
@debug str-insert($font, "italic ", 1);

.card { 
  font-size: unquote($font-size);
  font-family: quote($font-family);
}
```

*Respective Compilation Message:*

```bash
test\main.scss:7 DEBUG: 600
test\main.scss:8 DEBUG: 14px
test\main.scss:9 DEBUG: sans-serif
test\main.scss:10 DEBUG: 5
test\main.scss:11 DEBUG: SANS-SERIF
test\main.scss:12 DEBUG: italic 600 14px sans-serif
```

*Respective CSS Output:*

```css
.card {
  font-size: 600;
  font-family: "sans-serif";
}
```

*Note: Sass doesn't has built-in function for string replace.*

---
[&#8682; To Top](#-strings)

[&#10094; Previous Topic](./partials.md) &emsp; [Next Topic &#10095;](./meta-comments.md)

[&#8962; Goto Home Page](../README.md)