## &#10162; Sass Math:
Sass built-in module provide various functions to give possibilities for basic and required mathematical related operations.

### &#9780; Overview:
1. [Data types](#-data-types)
2. [Variables](#-variables)
3. [Identical Variables](#-identical-variables)
4. [Default Value](#-default-value)
5. [Built-in Variables](#-built-in-variables)
6. [Global Variables](#-global-variables)
7. [Local Variables](#-local-variables)
8. [Variable Shadowing](#-variable-shadowing)
9. [Control Variable with Flow Control](#-control-variable-with-flow-control)
10. [Unit Comparison](#-unit-comparison)
11. [Unit Check](#-unit-check)
12. [Minimum and Maximum Value](#-minimum-and-maximum-value)
13. [Operators](#-operators)
14. [Ceil Function](#-ceil-function)
15. [Floor Function](#-floor-function)
16. [Round Function](#-round-function)
17. [Absolute Function](#-absolute-function)
18. [Min and Max Functions](#-min-and-max-functions)
19. [Clamp Function](#-clamp-function)
20. [Division Function](#-division-function)
21. [Percentage Function](#-percentage-function)
22. [Random Function](#-random-function)
23. [Pow Function](#-pow-function)
24. [Log Function](#-log-function)
25. [Square Root Function](#-square-root-function)
26. [Hypot Function](#-hypot-function)
27. [Trigonometric Functions](#-trigonometric-functions)


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

### &#10022; Identical Variables:

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

### &#10022; Default Value:

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

### &#10022; Built-in Variables:

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

**Constants:**

```scss
@use 'sass:math';

@debug math.$e;
@debug math.$epsilon;
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 2.7182818285
test\main.scss:4 DEBUG: 0
```

### &#10022; Global Variables:

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

### &#10022; Local Variables:

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

### &#10022; Variable Shadowing:

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

### &#10022; Control Variable with Flow Control:

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


### &#10022; Unit Comparison:

Sass built-in math module provide functions to check and compare given numbers or values are compatible for manipulation and operations on it before proceed with it.

If both are compatible then it return boolean true otherwise boolean false.

```scss
@use 'sass:math';

$number1: 10px; 
$number2: 15px;
$number3: 2rem;

@debug math.compatible($number1, $number2);
@debug math.compatible($number1, $number3);
@debug comparable($number1, $number2);
@debug comparable($number1, $number3);
```

*Respective Compilation Message:*

```bash
test\main.scss:7 DEBUG: true
test\main.scss:8 DEBUG: false
test\main.scss:9 DEBUG: true
test\main.scss:10 DEBUG: false
```

### &#10022; Unit Check:

**Unit-less Check:**

Sass built-in math module provides function to check the given value is an unit-less.

```scss
@use 'sass:math';

$number1: 10px; 
$number2: 15;

@debug math.is-unitless($number1);
@debug unitless($number2);
```

*Respective Compilation Message:*

```bash
test\main.scss:6 DEBUG: false
test\main.scss:7 DEBUG: true
```

**Extract Unit:**

Sass built-in math module provides function to extract unit from the given value.

```scss
@use 'sass:math';

$number1: 10px; 
$number2: 15;

@debug math.unit($number1);
@debug unit($number2);
```

*Respective Compilation Message:*

```bash
test\main.scss:6 DEBUG: px
test\main.scss:7 DEBUG:
```

### &#10022; Minimum and Maximum Value:

Sass can represent maximum finite number as a 64-bit floating point number.

Sass can represent smallest positive number as a 64-bit floating point number. 

Sass numbers has 10 digits of precision, in many cases that to be 0.

```scss
@use 'sass:math';

@debug math.$min-number;
@debug math.$max-number;
@debug math.$max-safe-integer;
@debug math.$min-safe-integer;
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 0
test\main.scss:4 DEBUG: 179769313486231570000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
test\main.scss:5 DEBUG: 9007199254740991
test\main.scss:6 DEBUG: -9007199254740991
```

### &#10022; Operators:
It supports various operators for mathematical calculations, comparisons and logical operations. Ensure operants are compatible data types to perform calculations.

**Arithmetic Operators:**
- `+`: Addition
- `-`: Subtraction
- `*`: Multiplication
- `/`: Division (deprecated for math operation)
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

### &#10022; Ceil Function:

Sass built-in math module provides ceil function, which round up the given number to next highest whole number.

```scss
@use 'sass:math';

@debug math.ceil(5); 
@debug math.ceil(5.0001); 
@debug math.ceil(5.9);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 5
test\main.scss:4 DEBUG: 6
test\main.scss:5 DEBUG: 6
```

### &#10022; Floor Function:

Sass built-in math module provides function to round up the given number to next lowest whole number.

```scss
@use 'sass:math';

@debug math.floor(5); 
@debug math.floor(5.1); 
@debug math.floor(5.9999);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 5
test\main.scss:4 DEBUG: 5
test\main.scss:5 DEBUG: 5
```

### &#10022; Round Function:

Sass built-in math module provides function to round up the given number to possible nearest whole number.

```scss
@use 'sass:math';

@debug math.round(5.001);
@debug math.round(5.4999);
@debug math.round(5.5);
@debug math.round(5.9);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 5
test\main.scss:4 DEBUG: 5
test\main.scss:5 DEBUG: 6
test\main.scss:6 DEBUG: 6
```

### &#10022; Absolute Function:

Sass built-in math module provides function to get absolute value for given number. If the number is negative then it will return corresponding positive number. And it does not affect on positive numbers.

```scss
@use 'sass:math';

@debug math.abs(5.001);
@debug math.abs(-5.9);
@debug math.abs(-5);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 5.001
test\main.scss:4 DEBUG: 5.9
test\main.scss:5 DEBUG: 5
```


### &#10022; Min and Max Functions:

Sass built-in math module provide functions to get minimum value out of given list of values. At same for maximum value out of given list of values.

**Min Function:**

```scss 
@use 'sass:math';

$size: 12px 14px 16px 20px;

@debug math.min($size...);
@debug min(-5, 0, 6, 10, -30);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: 12px
test\main.scss:6 DEBUG: -30
```

**Max Function:**

```scss 
@use 'sass:math';

$size: 12px 14px 16px 20px;

@debug math.max($size...);
@debug max(-5, 0, 6, 10, -30);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: 20px
test\main.scss:6 DEBUG: 10
```

### &#10022; Clamp Function:

Sass built-in math module provides function to suggest minimum and maximum value for given value to be clamped if exceeds the range. If the given value is below the minimum value then it will return minimum value and vice versa.

```scss
@use 'sass:math';

@debug math.clamp(-5px, 0px, 10px);
@debug math.clamp(0, 110, 100);
@debug math.clamp(2rem, 1rem, 5rem);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 0px
test\main.scss:4 DEBUG: 100
test\main.scss:5 DEBUG: 2rem
```

### &#10022; Division Function:

Sass built-in math module provides function to make division operation on two given numbers. `/` operator is deprecated. 

```scss
@use 'sass:math';

@debug math.div(1, 2);
@debug math.div(20px, 2px);
@debug math.div(20px, 2);
@debug math.div(20px, 2s);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 0.5
test\main.scss:4 DEBUG: 10
test\main.scss:5 DEBUG: 10px
test\main.scss:6 DEBUG: 10px/s
```


### &#10022; Percentage Function:

Sass built-in math module provides function to calculate percentage for a given number. It accepts unit-less decimal numbers between 0 to 1.

```scss
@use 'sass:math';

@debug math.percentage(0.5);
@debug math.percentage(math.div(20px, 50px));
```

*Respective Compilation Message:* 

```bash
test\main.scss:3 DEBUG: 50%
test\main.scss:4 DEBUG: 40%
```

### &#10022; Random Function:

Sass built-in math module provides function to give random number. It give random between unit-less decimal value from 0 to 1 when the second argument `$limit` is missing or to be `null`. If the second argument `$limit` is passed then it consider for maximum value limit. 

If the `$limit` is greater than or equal to 1 then the random number will be a whole number. It ignores units.


```scss
@use 'sass:math';

@debug math.random();
@debug math.random($limit: null);
@debug math.random($limit: 1);
@debug math.random($limit: 100);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 0.3967614776
test\main.scss:4 DEBUG: 0.8615115526
test\main.scss:5 DEBUG: 1
test\main.scss:6 DEBUG: 52
```

### &#10022; Pow Function:

Sass built-in math module provides function to calculate logarithm value for given number with given base. It accepts both arguments to be an unit-less value. The exponent value may be either positive or negative.

```scss
@use 'sass:math';

@debug math.pow(10, 2); // calculates power of 10
@debug math.pow(10, -2); // calculates power of 1/10 due to negative exponent
@debug math.pow(64, math.div(1, 2)); // square root of 64
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 100
test\main.scss:4 DEBUG: 0.01
test\main.scss:5 DEBUG: 8
```

### &#10022; Log Function:

Sass built-in math module provides function to calculate power for given number with given exponent value. It accepts second argument as base value. If the base value `null` or not specified then it will calculate natural logarithmic value for the given number.

```scss
@use 'sass:math';

@debug math.log(100);
@debug math.log(100, 10);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 4.605170186
test\main.scss:4 DEBUG: 2
```

### &#10022; Square Root Function:

Sass built-in math module provides function to calculate square root of the given number. That number should be an unit-less value. If the number is negative then it would return `NaN` that is a not an number. Due to imaginary part of number.

```scss
@use 'sass:math';

@debug math.sqrt(64);
@debug math.sqrt(math.pow(10, 2));
@debug math.sqrt(-1);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 8
test\main.scss:4 DEBUG: 10
test\main.scss:5 DEBUG: NaN
```

### &#10022; Hypot Function:

Sass built-in math module has `hypot()` and which calculates length of n-dimensional vector by taking square-root of sum of square of the all values specified such as Square-root(a^2 + b^2 + c^2 + ...). It accepts both unit and unit-less values. But if it specified by different units then it considers and takes first value's unit.

```scss
@use 'sass:math';

@debug math.hypot(3, 4);
@debug math.hypot(3, 4, 5, 6);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 5
test\main.scss:4 DEBUG: 9.2736184955
```

### &#10022; Trigonometric Functions:

Sass built-in math module provide functions to work with trigonometric values.

**Sine:**

It calculates sine value of given number. The number must be an angle with compatible units of deg or rad. If the number has no units, then it is assumed to be in rad unit.

```scss
@use 'sass:math';

@debug math.sin(60deg);
@debug math.sin(1rad);
@debug math.sin(1);
@debug math.sin(math.div(1,2)); // 1/2 rad
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 0.8660254038
test\main.scss:4 DEBUG: 0.8414709848
test\main.scss:5 DEBUG: 0.8414709848
test\main.scss:6 DEBUG: 0.4794255386
```

**Cosine:**

It calculates cosine value of given number. The number must be an angle with compatible units of deg or rad. If the number has no units, then it is assumed to be in rad unit.

```scss
@use 'sass:math';

@debug math.cos(60deg);
@debug math.cos(1rad);
@debug math.cos(1);
@debug math.cos(math.div(1,2)); // 1/2 rad
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 0.5
test\main.scss:4 DEBUG: 0.5403023059
test\main.scss:5 DEBUG: 0.5403023059
test\main.scss:6 DEBUG: 0.8775825619
```

**Tangent:**

It calculates tangent value of given number. The number must be an angle with compatible units of deg or rad. If the number has no units, then it is assumed to be in rad unit.

```scss
@use 'sass:math';

@debug math.tan(60deg);
@debug math.tan(1rad);
@debug math.tan(1);
@debug math.tan(math.div(1,2)); // 1/2 rad
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 1.7320508076
test\main.scss:4 DEBUG: 1.5574077247
test\main.scss:5 DEBUG: 1.5574077247
test\main.scss:6 DEBUG: 0.5463024898
```

**ArcSine:**

It calculates arcsine value of given number in a degree. The number must be an unit-less.

```scss
@use 'sass:math';

@debug math.asin(0.8660254038);
@debug math.asin(1);
@debug math.asin(2);
@debug math.asin(0.3);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 60.0000000018deg
test\main.scss:4 DEBUG: 90deg
test\main.scss:5 DEBUG: NaNdeg
test\main.scss:6 DEBUG: 17.4576031237deg
```

**ArcCosine:**

It calculates arccosine value of given number in a degree. The number must be an unit-less.

```scss
@use 'sass:math';

@debug math.acos(0.5);
@debug math.acos(1);
@debug math.acos(2);
@debug math.acos(0.5403023059);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 60deg
test\main.scss:4 DEBUG: 0deg
test\main.scss:5 DEBUG: NaNdeg
test\main.scss:6 DEBUG: 57.2957795109deg
```

**ArcTangent:**

It calculates arctangent value of given number in a degree. The number must be an unit-less.

```scss
@use 'sass:math';

@debug math.atan(0.5);
@debug math.atan(-1);
@debug math.atan(2);
@debug math.atan(1.7320508076);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 26.5650511771deg
test\main.scss:4 DEBUG: -45deg
test\main.scss:5 DEBUG: 63.4349488229deg
test\main.scss:6 DEBUG: 60.0000000004deg
```

**ArcTangent with 2 argument:**

It calculates arctangent value of two argument numbers in a degree. The number must be a compatible units or an unit-less.

```scss
@use 'sass:math';

@debug math.atan2(1,2);
@debug math.atan2(-1,1);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: 26.5650511771deg
test\main.scss:4 DEBUG: -45deg
```

---
[&#8682; To Top](#-sass-math)

[&#10094; Previous Topic](./basic-syntax.md) &emsp; [Next Topic &#10095;](./nesting.md)

[&#8962; Goto Home Page](../README.md)