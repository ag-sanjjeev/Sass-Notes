## &#10162; Mixins:
Sass has a powerful feature called Mixins that allow to create reusable blocks of style. It reduce code redundancy and improve maintainability.

A mixin name might be any of the Sass identifier. But it doesn’t begin with `--`. Their name with hyphens and underscore are identical like `@mixin rounded-border($r) {...}` and `@mixin rounded_border($r) {...}` are same.

It can contain any statements other than top-level statements. 

Mixins can keep tracks both positional and keyword arguments. To pass both at once might possible. It is a good practice to pass arguments by position rather than by argument name. But it is depends on number of arguments and optional default argument value.

Thus it encapsulates the styles into a single style rule.

### &#9780; Overview:
1. [Mixin Declaration](#-mixin-declaration)
2. [Utilize Mixin](#-utilize-mixin)
3. [Mixin with Arguments](#-mixin-with-arguments)
4. [Mixin with Default Argument Value](#-mixin-with-default-argument-value)
5. [Keyword Argument](#-keyword-argument)
6. [N Number of Arguments](#-n-number-of-arguments)
7. [Arbitrary Keyword](#-arbitrary-keyword)
8. [Passing Arbitrary Arguments](#-passing-arbitrary-arguments)
9. [Nested Mixins](#-nested-mixins)
10. [Passing Argument to Content Block](#-passing-argument-to-content-block)
11. [Indented Mixins](#-indented-mixins)
12. [Comparison with functions](#-comparison-with-functions)

### &#10022; Mixin Declaration:

Declare mixin using the `@mixin` directive followed by the required mixin name. The mixin body contains the styles to be included.

```scss
@mixin reset {
  margin: 0;
  padding: 0;  
}
```

### &#10022; Utilize Mixin:

To utilize a declared mixin, by the `@include` directive followed by the required mixin name:

```scss
.list {
  @include reset;
}
```

*Respective CSS Output:*

```css
.list {
  margin: 0;
  padding: 0;
}
```

### &#10022; Mixin with Arguments:

It is possible to create more flexible mixins by passing arguments. It allows to customize the output of the mixin based on argument values.

```scss
@mixin border-radius($radius) {
  border-radius: $radius;
}

.card {
  @include border-radius(5px);
}

.circle {
  @include border-radius(50%);
}
```

*Respective CSS Output:*

```css
.card {
  border-radius: 5px;
}

.circle {
  border-radius: 50%;
}
```

### &#10022; Mixin with Default Argument Value:

It is possible to set default argument value for the mixins. It allows to set default style output if the argument value missing or not specified.

```scss
@mixin border-radius($radius:0px) {
  border-radius: $radius;
}

.card {
  @include border-radius;
}

.circle {
  @include border-radius(50%);
}
```

*Respective CSS Output:*

```css
.card {
  border-radius: 0px;
}

.circle {
  border-radius: 50%;
}
```

### &#10022; Keyword Argument:

It is possible to specify parameter value before with their argument name for the mixins. It allows to set values to specified argument.

```scss
@mixin shape($width, $height, $radius:0px) {
  width: $width;
  height: $height;

  @if $radius != 0 {
    border-radius: $radius;
  }
}

.card {
  @include shape($width:200px, $height: 100px, $radius: 10px);
}

.circle {
  @include shape($width: 100px, $height: 100px, $radius: 100px);
}
```

*Respective CSS Output:*

```css
.card {
  width: 200px;
  height: 100px;
  border-radius: 10px;
}

.circle {
  width: 100px;
  height: 100px;
  border-radius: 100px;
}
```

### &#10022; N number of arguments:

Sass Mixin can accept N number of arguments by adding continuous three dot `...` immediate after with argument name to accept those parameters.

```scss
@mixin masonry($height, $selectors...) {
  @for $i from 0 to length($selectors) {
    .masonry#{nth($selectors, $i + 1)} { 
      aspect-ratio: 1;     
      min-height: $height;
    }
  }
}

@include masonry(200px, ".image1", ".image2", ".image3");
``` 

*Respective CSS Output:*

```css
.masonry.image1 {
  aspect-ratio: 1;
  min-height: 200px;
}

.masonry.image2 {
  aspect-ratio: 1;
  min-height: 200px;
}

.masonry.image3 {
  aspect-ratio: 1;
  min-height: 200px;
}
```

### &#10022; Arbitrary Keyword:

`meta.keywords()` function takes the argument list where the mixin gets invoked with argument list.

```scss
@use "sass:meta";

@mixin buttons($args...) {
  @debug meta.keywords($args);  

  @each $name, $color in meta.keywords($args) {
    button.btn-#{$name} {
      background-color: $color;
    }
  }
}

@include buttons(
  $primary: #1976D2,
  $secondary: #6D4C41,
  $success: #43A047,
  $warning: #FFEB3B,
  $danger: #F44336
);
``` 

*Respective Compilation Message:*

```bash
test\main.scss:4 DEBUG: (primary: #1976D2, secondary: #6D4C41, success: #43A047, warning: #FFEB3B, danger: #F44336)
```

*Respective CSS Output:*

```css
button.btn-primary {
  background-color: #1976D2;
}

button.btn-secondary {
  background-color: #6D4C41;
}

button.btn-success {
  background-color: #43A047;
}

button.btn-warning {
  background-color: #FFEB3B;
}

button.btn-danger {
  background-color: #F44336;
}
```

### &#10022; Passing Arbitrary Arguments:

To pass a list of arbitrary arguments with a Sass variable rather than mentioning as traditional list of parameters.

```scss
@mixin masonry($height, $selectors...) {
  @for $i from 0 to length($selectors) {
    .masonry#{nth($selectors, $i + 1)} { 
      aspect-ratio: 1;     
      min-height: $height;
    }
  }
}

$masonry-items: ".image1", ".image2", ".image3";
@include masonry(200px, $masonry-items...);
```

*Respective CSS Output:*

```css
.masonry.image1 {
  aspect-ratio: 1;
  min-height: 200px;
}

.masonry.image2 {
  aspect-ratio: 1;
  min-height: 200px;
}

.masonry.image3 {
  aspect-ratio: 1;
  min-height: 200px;
}
```

### &#10022; Nested Mixins:

It is possible to include mixin inside another mixin. 

```scss
@mixin border-radius($radius) {
  @if $radius != 0 {
    border-radius: $radius;
  }
}

@mixin shape($width, $height, $radius:0px) {
  width: $width;
  height: $height;

  @include border-radius($radius);
}

.card {
  @include shape($width:200px, $height: 100px);
}

.circle {
  @include shape($width: 100px, $height: 100px, $radius: 100px);
}
```

*Respective CSS Output:*

```css
.card {
  width: 200px;
  height: 100px;
  border-radius: 0px;
}

.circle {
  width: 100px;
  height: 100px;
  border-radius: 100px;
}
```

**Deprecated Mixin Definition:**

```scss
@mixin reset {
  @warn "The reset mixin is deprecated. Rather than use reset-all.";
  @include reset-all;
}
```

*Respective Compilation Message:*

```bash
WARNING: The reset mixin is deprecated. Rather than use reset-all.
    test\main.scss 2:3   reset()
    test\main.scss 13:2  root stylesheet
```

*Respective CSS Output:*

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

### &#10022; Passing Argument to Content Block:
Mixins can passes arguments to their content block, But it needs to define content block that accept those arguments.

```scss
@mixin media($types...) {
  @each $type in $types {
    @media #{$type} {
      @content($type);
    }
  }
}

@include media(screen, print) using ($type) {
  body {    
    font-family: 'Open Sans', sans-serif;
    @if $type == print {
      margin: 1cm 1.5cm;
    }
  }
}
```

*Respective CSS Output:*

```css
@media screen {
  body {
    font-family: "Open Sans", sans-serif;
  }
}
@media print {
  body {
    font-family: "Open Sans", sans-serif;
    margin: 1cm 1.5cm;
  }
}
```

### &#10022; Indented Mixins:
Indented Mixins are follows different ways to declare. Such as `@mixin <name> {...}` can be declared with `=<name>` and `@include <name>;` can be utilized as `+<name>`.

```sass
=reset
 margin: 0
 padding: 0
 box-sizing: border-box

body
 +reset
 font-family: 'Open Sans', sans-serif
``` 

*Respective CSS Output:*

```css
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Open Sans", sans-serif;
}
```

### &#10022; Comparison with functions:
Both mixins and functions can be used for utilize reusable code, But differs in some features.

**Mixins:**
- It creates directly CSS style output.
- It cannot return values.
- It is primarily used for styling.

**Functions:**
- It can perform calculations and manipulations.
- It can return values.
- It cannot create directly CSS style output but used for dynamic calculations, color manipulation, or generating CSS property values.

**Example:**

```scss
// Mixin Declaration
@mixin border-radius($radius) {
  border-radius: $radius;
}

// Function Declaration
@function pixel2rem($px) {
  @return $px / 16 + rem;
}
```

---
[&#8682; To Top](#-mixins)

[&#10094; Previous Topic](./meta-comments.md) &emsp; [Next Topic &#10095;](./placeholders.md)

[&#8962; Goto Home Page](../README.md)