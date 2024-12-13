## &#10162; Sass Math:
Sass will provide possibilities for basic and required mathematical related properties and operations.

### &#9780; Overview:
1. [Data types](#-data-types)
2. [Variables](#-variables)
3. [Operators](#-operators)

### &#10022; Data Types:
Sass primarily deals with two kinds of data types:
1. Numbers:
	- Integers
	- Decimals
	- Percentages
	- Units (e.g., px, em, rem) 
		- Pixels
		- Ems
		- Rems
		- Other units
2. Strings:
	- Textual data enclosed in quotes single or double
3. Colors: 
	- Hex color
	- RGB color
	- HSL color
	- Named color
4. Lists
5. Maps

### &#10022; Variables:
Sass variable declaration looks a like property declaration. But it stores values that can be reused throughout project styles. It is defined using the `$` symbol.

```scss
$primary-color: #E7E7E7;
$border-primary: rgba($primary-color, 0.8);
$font-size: 14px;
```

*Respective CSS Output:*

```css
.card {
  background-color: white;
  color: #E7E7E7;
  border-color: rgba(231, 231, 231, 0.8);
  font-size: 14px;
}
```

**Variable Usage:**

```scss
.rectangle {
  $size: 100px;
  width: $size * 2;
  height: $size;
}

.circle {
	$size: 100px;
	width: $size;
	height: $size;
	border-radius: $size * 0.5;
}
```

*Respective CSS Output:*

```css
.rectangle {
  width: 200px;
  height: 100px; 
}

.circle {
  width: 100px;
  height: 100px;
  border-radius: 50px;
}
```

**Identical Variables:**

Sass treats variables with hyphens `-` and underscore `_` as same. And it is identical. For example, `$font-size` and `$font_size` are referred as same. In early days, Sass supports only underscore. In later, Sass provides support for hyphens to deal with CSS properties and migration purpose.

```scss
$font-size: 14px;

p {
	font-size: $font_size;
}
```

*Respective CSS Output:*

```css
p {
  font-size: 14px;
}
```

**Default Value:**

It allow to assign value to a variables only if that are null or not defined before. Otherwise, It would not allow to overwrite. Default value can be defined with `!default` flag.

```scss
$font-size: 14px;

p {
	$font-size: 15px !default;
	font-size: $font-size;
}
```

*Respective CSS Output:*

```css
p {
  font-size: 14px;
}
```

**Built-in Variables:**

Built-in variables are defined in the built-in modules. Which cannot be overwritten.

```scss
@use "sass:math" as math;

// Cannot overwrite
math.$pi: 0;
```

*Respective Compilation Message:*

```bash
Error: Cannot modify built-in variable.
  ╷
4 │ math.$pi: 0;
  │ ^^^^^^^^^^^
  ╵
  test\main.scss 4:1  root stylesheet
```

**Global Variables:**

Variables declared in the top level of stylesheet is referred as global variables. It can be accessed throughout stylesheet.

```scss
$global-variable: level global;

.selector {
  global: $global-variable;
}

.another-selector {
  global: $global-variable;
}
```

*Respective CSS Output:*

```css
.selector {
  global: level global;
}

.another-selector {
  global: level global;
}
```

**Local Variables:**

Variables declared in the specific scope level of stylesheet is referred as local variables. It can be accessed within the scope.

```scss
.selector {
  $local-variable: level local;
  local: $local-variable;
}

.another-selector {
	local: $local-variable;
}
```

*Respective Compilation Message:*

```bash
Error: Undefined variable.
  ╷
7 │     local: $local-variable;
  │            ^^^^^^^^^^^^^^^
  ╵
  test\main.scss 7:9  root stylesheet
```

**Variable Shadowing:**

It gives possibilities to create local variable with same name of global variable without affecting and conflict their values.

```scss
$variable: level global;

.selector {
	$variable: level local;
	property: $variable;
}

.another-selector {
	property: $variable;
}
```

*Respective CSS Output:*

```css
.selector {
  property: level local;
}

.another-selector {
  property: level global;
}
```

To overwrite value to the global variable by assign a value with `!global` flag.

```scss
$variable: level global;

.selector {
	$variable: level local !global;
	property: $variable;
}

.another-selector {
	property: $variable;
}
```

*Respective CSS Output:*

```css
.selector {
  property: level local;
}

.another-selector {
  property: level local;
}
```

**Control Variable with Flow Control:**

Using control flow logic to change variable value.

```scss
$dark-theme: true !default;
$primary-color: #81D4FA !default;
$secondary-color: #E0E0E0 !default;

@if $dark-theme {
  $primary-color: darken($primary-color, 50%);
  $secondary-color: lighten($secondary-color, 50%);
}

.card {
  background-color: $primary-color;
  box-shadow: 1px 1px solid $secondary-color;
}
```

*Respective CSS Output:*

```css
.card {
  background-color: #055377;
  box-shadow: 1px 1px solid white;
}
```

### &#10022; Operators:
It supports various operators for mathematical calculations, comparisons and logical operations. Ensure operants are compatible data types to perform calculations.

**Arithmetic Operators:**
- `+`: Addition
- `-`: Subtraction
- `*`: Multiplication
- `/`: Division
- `%`: Modulus

**Comparison Operators:**
- `>`: Greater than
- `<`: Less than
- `>=`: Greater than or equal to
- `<=`: Less than or equal to
- `==`: Equal to
- `!=`: Not equal to

**Logical Operators:** 
- `and`: Logical AND operator
- `or`: Logical OR operator
- `not`: Logical NOT operator

*Example:*
```scss
$base-font-size: 14px;
$line-height: 1.5;

body {
  font-size: $base-font-size;
  line-height: $line-height;
}

h1 {
  font-size: $base-font-size * 2;
  line-height: $line-height;
}
```

---
[&#8682; To Top](#-sass-math)

[&#10094; Previous Topic](./basic-syntax.md) &emsp; [Next Topic &#10095;](./nesting.md)

[&#8962; Goto Home Page](../README.md)