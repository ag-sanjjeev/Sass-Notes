## &#10162; Control Directives:

Sass provide the ability and possibility to control the compilation process flow in the desired manner. 

It can control the flow by applying conditional logic as well as iteration. This will simplifies the logic and style rules.

When comes to control directives, boolean `true` is always **truth**. But boolean `false` and `null` value are treat as **false**.

### &#9780; Overview:
1. [Control Flow Statements](#-control-flow-statements)
2. [IF Statement](#-if-statement)
3. [ELSE Statement](#-else-statement)
4. [ELSE IF Statement](#-else-if-statement)
5. [Loops](#-loops)
6. [FOR Through Loop](#-for-through-loop)
7. [FOR To Loop](#-for-to-loop)
8. [EACH Loop](#-each-loop)
9. [EACH Loop Destructuring](#-each-loop-destructuring)
10. [WHILE Loop](#-while-loop)

### &#10022; Control Flow Statements:

Control Flow Statements can control the direction of compilation process when met the given condition to be boolean true.

List of control flow statements in Sass:
1. `@if`
2. `@else`
3. `@else if`

### &#10022; IF Statement:

`@if` statements execute a block of code only if a given condition is boolean true.

*Syntax:*

```scss
@if <condition> {
  // Code to execute
}
```

*Example:*

```scss
$is-theme-dark: true;

body {
  @if $is-theme-dark {
    background-color: black;
    color: white; 
  } 
}
```

*Respective CSS Output:*

```css
body {
  background-color: black;
  color: white;
}
```

### &#10022; ELSE Statement:

`@if` statements execute a block of code only if a given condition is boolean true. 
Otherwise `@else` statements executes a block of code.

*Syntax:*

```scss
@if <condition> {
  // Code to execute
} @else {
  // Code to execute
}
```

*Example:*

```scss
$is-theme-dark: false;

body {
  @if $is-theme-dark {
    background-color: black;
    color: white; 
  } @else {
    background-color: white;
    color: black;
  }
}
```

*Respective CSS Output:*

```css
body {
  background-color: white;
  color: black;
}
```

### &#10022; ELSE IF Statement:

`@if` statements execute a block of code only if a given condition is boolean true. If it is boolean false, then it will move on to the next `@else if` statements to execute a block of code only if a given condition is boolean true as same.

*Syntax:*

```scss
@if <condition1> {
  // Code to execute
} @else if <condition2> {
  // Code to execute
} @else {
  // Code to execute
}
```

*Example:*

```scss
$theme: primary;

body {
  @if $theme == dark {
    background-color: black;
    color: white; 
  } @else if $theme == primary {
    background-color: purple;
    color: white;
  } @else {
    background-color: white;
    color: black;
  }
}
```

*Respective CSS Output:*

```css
body {
  background-color: purple;
  color: white;
}
```

### &#10022; Loops:

Sass provides loops that can iterate over repeated block of code or style rules. This will reduces number of lines to be repeated in stylesheet.

List of Loops in Sass:
1. `@for`
2. `@each`
3. `@while`

Comparatively, `@for` and `@each` are clean and **faster** to compile. But `@while` are required for few complex logic.

### &#10022; FOR Through Loop:

`@for` loop executes a block of code for a specified number of iterations until it reaches end limit or expression. 

This loop uses `through` statement in between start and end of the limit. This takes end of the limit as well. 

*Syntax:*

```scss
@for $i from <start> through <end> {
  // Code to execute
}
```

*Example:*

```scss
$carry: 0;
@for $i from 0 through 2 {
  li:nth-child(#{$i}) {
    color: blue;
    $carry: $carry + $i;
    padding-left: unquote($carry * 2 + 'px');
  }
}
```

*Respective CSS Output:*

```css
li:nth-child(0) {
  color: blue;
  padding-left: 0px;
}

li:nth-child(1) {
  color: blue;
  padding-left: 2px;
}

li:nth-child(2) {
  color: blue;
  padding-left: 4px;
}
```

### &#10022; FOR To Loop:

`@for` loop executes a block of code for a specified number of iterations before reaching the end limit or expression. 

This loop uses `to` statement in between start and end of the limit. This excludes end of the limit. 

*Syntax:*

```scss
@for $i from <start> to <end> {
  // Code to execute
}
```

*Example:*

```scss
$carry: 0;
@for $i from 0 to 2 {
  li:nth-child(#{$i}) {
    color: blue;
    $carry: $carry + $i;
    padding-left: unquote($carry * 2 + 'px');
  }
}
```

*Respective CSS Output:*

```css
li:nth-child(0) {
  color: blue;
  padding-left: 0px;
}

li:nth-child(1) {
  color: blue;
  padding-left: 2px;
}
```

### &#10022; EACH Loop:

`@each` loop iterates over a given list or a map.
    
**Iterate a list:**

*Syntax:*

```scss
@each $item in <list> {
  // Code to execute
}
```

*Example:*

```scss
$colors: 'red' 'green' 'blue';

@each $color in $colors {
  .button-#{quote($color)} {
    background-color: unquote($color);
  }
}
```

*Respective CSS Output:*

```css
.button-red {
  background-color: red;
}

.button-green {
  background-color: green;
}

.button-blue {
  background-color: blue;
}
```

**Iterate a map:**

*Syntax:*

```scss
@each $key, $value in $map {
  // Code to execute
}
```

*Example:*

```scss
$colors: ("primary": blue, "success": green, "danger": red);

@each $key, $value in $colors {
  .button-#{$key} {
    background-color: $value;
  }
}
```

*Respective CSS Output:*

```css
.button-primary {
  background-color: blue;
}

.button-success {
  background-color: green;
}

.button-danger {
  background-color: red;
}
```

### &#10022; EACH Loop Destructuring:

When it is required to iterate a list having another list as a item. Then Destructuring will help to iterate those list of list items.

```scss
$borders:
  "primary" 1px solid blue,
  "success" 1px solid green,
  "danger" 2px dashed red;

@each $name, $width, $style, $color in $borders {
  .border-#{$name} {
    border: $width $style $color;
  }
}
```

*Respective CSS Output:*

```css
.border-primary {
  border: 1px solid blue;
}

.border-success {
  border: 1px solid green;
}

.border-danger {
  border: 2px dashed red;
}
```

### &#10022; WHILE Loop:

`@while` loop will iterate until the condition or expression gets boolean `true`. Once, condition or expression gets boolean `false` then stops proceeding further.

```scss
$typography: 36px;
$size-limit: 6px;
$i: 1;

@while $typography >= $size-limit {
  h#{$i} {
    font-size: $typography;
  }
  $typography: $typography - $size-limit;
  $i: $i + 1;
}
```

*Respective CSS Output:*

```css
h1 {
  font-size: 36px;
}

h2 {
  font-size: 30px;
}

h3 {
  font-size: 24px;
}

h4 {
  font-size: 18px;
}

h5 {
  font-size: 12px;
}

h6 {
  font-size: 6px;
}
```

---
[&#8682; To Top](#-control-directives)

[&#10094; Previous Topic](./functions.md) &emsp; [Next Topic &#10095;](./maps-and-lists.md)

[&#8962; Goto Home Page](../README.md)