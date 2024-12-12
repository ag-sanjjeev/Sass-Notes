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
It allow to store values that can be reused throughout project styles. It is defined using the `$` symbol.

```scss
$primary-color: #E7E7E7;
$font-size: 14px;
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