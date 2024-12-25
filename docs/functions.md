## &#10162; Functions:
Sass provides function feature like programmatic approach to the CSS styles. Which gives possibilities to use built-in functions available in Sass as well as define custom one.

Sass function might accept arguments and return values.

Sass allow to define and perform complex operations on values that you can be used throughout the stylesheet.

Sass function name doesn't begin with double hyphens `--`. Sass function treats both hyphens `-` and underscore `_` in their name.

Sass can possible to manipulate global values. But it is not recommended in functions to manipulate or affect the global value. Sass functions recommended to use for performing calculations. Use mixins to affect and manipulate global value.

Sass function can accepts arguments both positional arguments and named or keyword arguments values like [mixins](./mixins.md).

Sass function can accepts arbitrary arguments like [mixins](./mixins.md#-arbitrary-keyword).

### &#9780; Overview:
1. [Function Declaration](#-function-declaration)
2. [Function Call](#-function-call)
3. [Function Arguments](#-function-arguments)
4. [Built-in Functions](#-built-in-functions)

### &#10022; Function Declaration:

Custom Sass functions can be declared by starts with `@function` rule followed by function name. That function name should be a standard naming conventions followed by Sass.

```scss
@use "sass:math";

@function pixel2rem($px) {
  @return math.div($px,16) + rem;
}
```

### &#10022; Function Call:

```scss
h1 {
  font-size: pixel2rem(16);
}
```

*Respective CSS Output:*

```css
h1 {
  font-size: 1rem;
}
```

### &#10022; Function Arguments:

Sass Function arguments can accept multiple arguments and it may have ___trailing commas___ to avoid errors when refactoring stylesheet.

Optionally, it may have default value argument or optional value argument. But default value argument can be declared with `argument name` followed by colon `:` and value.

*Function without trailing commas:*

```scss
@function sum($value1, $value2) {
  $sum: $value1 + $value2;
  @return $sum;
}

@debug sum(1,2);
```

*Function with trailing commas:*

```scss
@function sum($value1, $value2,) {
  $sum: $value1 + $value2;
  @return $sum;
}

@debug sum(1,2);
```

*Respective Compilation Message:*

Note: That both function definitions will give same output.

```bash
test\main.scss:8 DEBUG: 3
```

### &#10022; Built-in Functions:
Sass has varieties of built-in functions to be utilized for manipulate and to handle colors, lists, numbers and strings.

- **Color Functions:**
  - `lighten($color, $amount)`: Lightens a color.
  - `darken($color, $amount)`: Darkens a color.
  - `saturate($color, $amount)`: Increases the saturation of a color.
  - `desaturate($color, $amount)`: Decreases the saturation of a color.
  - `adjust-hue($color, $degrees)`: Adjusts the hue of a color.
- **String Functions:**
  - `str-index($string, $find)`: Returns the index of a substring within a string.
  - `str-insert($string, $toInsert, $index)`: Inserts a string at a specific index.
  - `str-length($string)`: Returns the length of a string.
  - `str-slice($string, $start-index, $end-index)`: Extracts a substring from a string.
  - `to-lower-case($string)`: Converts a string to lowercase.
  - `to-upper-case($string)`: Converts a string to uppercase.
  - `unquote($string)`: Removes quotes from a string.
  - `quote($string)`: Adds quotes to a string.
  - See More about [String](./strings.md)
- **Number Functions:**
  - `round($number)`: Rounds a number to the nearest integer.
  - `ceil($number)`: Rounds a number up to the nearest integer.
  - `floor($number)`: Rounds a number down to the nearest integer.
  - `abs($number)`: Returns the absolute value of a number.
  - `min($numbers)`: Returns the minimum value from a list of numbers.
  - `max($numbers)`: Returns the maximum value from a list of numbers.
  - See More about [Sass Math](./sass-math.md)

---
[&#8682; To Top](#-functions)

[&#10094; Previous Topic](./placeholders.md) &emsp; [Next Topic &#10095;](./control-directives.md)

[&#8962; Goto Home Page](../README.md)