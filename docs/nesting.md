## &#10162; Nesting:
It is one of the important features in Sass. Which will allows to nest CSS selectors, making code more readable and maintainable. This feature helps and improve to organize styles and avoid repetitive selectors and code.

### &#9780; Overview:
1. [Basic Nesting](#-basic-nesting)
2. [Advanced Nesting](#-advanced-nesting)
3. [Selectors](#-selectors)
4. [Properties and Values](#-properties-and-values)

### &#10022; Basic Nesting:
All children can be target for style using nesting from their parent code block.

```scss
.container {
  .box {
    padding: 10px 15px;
    border: 1px solid #E7E7E7;
  }
}
```

*Respective CSS Output:*
```css
.container .box {
  padding: 10px 15px;
  border: 1px solid #E7E7E7;
}
```

**Nesting with Pseudo-classes and Pseudo-elements:**

```scss
.link {
  &:hover {
    color: blue;
  }

  &:active {
  	color: white;
    background-color: blue;
  }
}
```

*Respective CSS Output:*
```css
.link:hover {
  color: blue;
}
.link:active {
  color: white;
  background-color: blue;
}
```

### &#10022; Advanced Nesting:
Nesting styles based on special requirements

**Adding Suffixes:**

This technique will add suffixes to the existing selectors such as `class`, `ID`, and `attribute`.

```scss
.hero {
	min-width: 300px;
  width: 1200px;
	max-width: 100%;
  margin: 1rem auto;  
  
  &__navigation {
    display: inline;    
    font-size: 14px;   

    &-link {
      display: block;
    }
  }
}
```

*Respective CSS Output:*

```css
.hero {
  min-width: 300px;
  width: 1200px;
  max-width: 100%;
  margin: 1rem auto;
}
.hero__navigation {
  display: inline;
  font-size: 14px;
}
.hero__navigation-link {
  display: block;
}
```

**Adding Parent Selector Prefix:**

Parent selector `&` will return the name when under parent styles. Otherwise, it will return null. Which is false that would not be rendered.

```scss
SCSS SYNTAX
@mixin font-style($style) {
  #{if(&, '&.text', '.text')} {
    font-style: #{$style};
  }
}

@include font-style('normal');

div {
  @include font-style('italic');
}
```

*Respective CSS Output:*

```css
.text {
  font-style: normal;
}

div.text {
  font-style: italic;
}
```

**Advanced Nesting with Sass Selector:**

Sass Selector and Parent Selector `&` with `@at-root` rule can give possibilities to interpolate parent selector. 

To match a selector with outer selector and an element, It is possible with `selector.unify()` function from Sass selector. 

The `selector.unify()` function will returns a selector that matches between two of the selectors intersection.

```scss
@use "sass:selector";

@mixin unify-parent($child) {
  @at-root #{selector.unify(&, $child)} {
    @content;
  }
}

div.container .item {
  @include unify-parent("h1") {
    padding: 0.5rem 1rem;
    background-color: blue;
    color: white;
  }
  @include unify-parent("p") {
    font-size: 14px;
    color: blue;
  }
}
```

*Respective CSS Output:*

```css
div.container h1.item {
  padding: 0.5rem 1rem;
  background-color: blue;
  color: white;
}

div.container p.item {
  font-size: 14px;
  color: blue;
}
```

### &#10022; Selectors:
Sass might supports all standard CSS selectors, including:
- `Type selectors:` `div`, `h1`, `p`, etc.
- `Class selectors:` `.class-name`
- `ID selectors:` `#id-name`
- `Attribute selectors:` `[attribute-name="value"]`
- `Pseudo-classes:` `:active`, `:focus`, `:hover`, `:not`, etc.
- `Pseudo-elements:` `::before`, `::after`

**Nesting with Parent Selectors:**

Use the `&` symbol to refer the parent selector for current child.

```scss
.nav {
  li {
    display: inline-block;
    a {
      color: blue;
      &:hover {
        color: white;
        background-color: blue;
      }
    }
  }
}
```

*Respective CSS Output:*

```css
.nav li {
  display: inline-block;
}
.nav li a {
  color: blue;
}
.nav li a:hover {
  color: white;
  background-color: blue;
}
```

**Placeholder selector:**

These types of selector is neither included in the CSS Style nor a style rule.

```scss
.a, %link {
  color: blue;
}

%link:hover {
  color: red;
}
``` 

*Respective CSS Output:*

```css
.a {
  color: blue;
}
```

**Unquote Selector Value:**

`unquote` function will remove any quotation marks specified in their argument list.

```scss
@debug (unquote("button") unquote(".icon"));
```

*Respective Compilation Message:*

```bash
test\main.scss:1 DEBUG: button .icon
```

**Check Super Selector:**

`is-superselector` function will return boolean value for given super selector and sub-selector.

`is-superselector($super, $sub)` will accept two argument. The first one will be super selector value and second one will be sub-selector value. Thus, it checks whether sub-selector is falls under specified super selector and return boolean true if it is, otherwise boolean false.

```scss
@use 'sass:selector';

@debug selector.is-superselector("button", "button");
@debug selector.is-superselector("button", "button.active");
@debug selector.is-superselector("button", ".active");
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: true
test\main.scss:4 DEBUG: true
test\main.scss:5 DEBUG: false
```

**Other Selector Functions:**
- `selector.append()`
- `selector.extend()`
- `selector.nest()`
- `selector.parse()`
- `selector.replace()`
- `selector.simple-selectors()`
- `selector.unify()`


### &#10022; Properties and Values:
Sass supports almost all standard CSS properties and values. Use variables to store values and reuse throughout stylesheet to assign value to properties.

**Property Interpolation:**

A property name can be interpolated, which give possibilities to dynamically generate properties as per requirement. Even an entire property name can be interpolated.

Sass starts parses selectors after successful parsing of interpolation. 

```scss
@mixin property-prefix($property, $value, $prefixes) {
  @each $prefix in $prefixes {
    -#{$prefix}-#{$property}: $value;
  }
  #{$property}: $value;
}

.blur {
  @include property-prefix(filter, blur(50%), moz webkit);
}
```

*Respective CSS Output:*

```CSS
.blur {
  -moz-filter: blur(50%);
  -webkit-filter: blur(50%);
  filter: blur(50%);
}
```

**Property Interpolation With Quoted String:**

When using interpolation, which removes quotes from strings value. It affects quoted strings which come from Sass variables. To use quoted string by the `meta.inspect()` function to preserve the quotes.

```scss
@use "sass:meta";

$font-family-sans-serif: system-ui, -apple-system, Roboto, "Helvetica Neue", Arial, sans-serif;
$font-family-monospace: SFMono-Regular, Menlo, Monaco, Consolas, "Courier New", monospace;

:root {
  --font-family-sans-serif: #{meta.inspect($font-family-sans-serif)};
  --font-family-monospace: #{meta.inspect($font-family-monospace)};
}
```

*Respective CSS Output:*

```css
:root {
  --font-family-sans-serif: system-ui, -apple-system, Roboto, "Helvetica Neue", Arial, sans-serif;
  --font-family-monospace: SFMono-Regular, Menlo, Monaco, Consolas, "Courier New", monospace;
}
```

**Property Declaration Nesting:**

Sass give possibilities to nest property declaration. Most of the CSS properties start with the same prefix such as margin property has margin-top, margin-right, margin-bottom and margin-left. Which is acts like namespace. This can be done by adding hyphen to the property name to nest other properties related to it.

```scss
.button {
  color: blue;
  background-color: transparent;
  transition: {
    property: all;
    duration: 1s;
    delay: 0.5s;
  }

  &:hover { 
  	color: white; 
  	background-color: blue; 
  }
}
```

*Respective CSS Output:*

```css
.button {
  color: blue;
  background-color: transparent;
  transition-property: all;
  transition-duration: 1s;
  transition-delay: 0.5s;
}
.button:hover {
  color: white;
  background-color: blue;
}

```

**Shorthand Property Declaration Nesting:**

Some of the CSS properties might have shorthand declaration. Such as contains both default value and explicit nested properties for the specific property.

```scss
.card {
  margin: auto {
    top: 10px;
    bottom: 5px;
  }
}
```

*Respective CSS Output:*

```css
.card {
  margin: auto;
  margin-top: 10px;
  margin-bottom: 5px;
}
```

**Hidden Property Declarations:**

To make some properties to be not consider when compile. But it is required when need. It is possible to declare hidden property by setting their value is null or an empty unquoted string, Then Sass would not compile those declaration at all.

```scss
$rounded-corners: false;

.card {
  border: 1px solid blue;
  border-radius: if($rounded-corners, 10px, null);
}
```

*Respective CSS Output:*

```css
.card {
  border: 1px solid blue;
}
```

**Show Parent Selector:**

It returns the current parent selector as it is, with a special expression. This will useful when debugging and maintenance.

```scss
.nav a:hover,
.sidebar .menu a:hover {
  parent-selector: &;  
}
```

*Respective CSS Output:*

```css
.nav a:hover,
.sidebar .menu a:hover {
  parent-selector: .nav a:hover, .sidebar .menu a:hover;
}
```

---
[&#8682; To Top](#-nesting)

[&#10094; Previous Topic](./sass-math.md) &emsp; [Next Topic &#10095;](./partials.md)

[&#8962; Goto Home Page](../README.md)