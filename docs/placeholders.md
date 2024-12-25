## &#10162; Placeholders:
Sass has a special kind of selector called `placeholder`. This behavior same as a class selector, but it starts with a percentage symbol `%`.

When it is declared but would not compiled into CSS output until it been extended. 

It same like a [mixins](./mixins.md) that contains set of style rules, but it doesn't accept any arguments. 

It can extend and apply style rules as well as their pseudo selectors style rule only if defined.

`@extend` rule and Placeholder will be compiled and resolved after all other style rules is compiled. Exactly, after their parent selectors compiled and resolved.  

It can handles and ensures the combinators, pseudo-classes and universal selectors that contain selectors.

Sass has selector function similar to `@extend` rule is `selector.extend()` function. But it works on a single selector.

If multiple selectors are extended then it will match every rule and combine that together.

### &#9780; Overview:
1. [Placeholder Declaration](#-placeholder-declaration)
2. [Extending Placeholders](#-extending-placeholders)
3. [Extending Multiple Placeholders](#-extending-multiple-placeholders)
4. [Private Placeholders](#-private-placeholders)
5. [Optional Placeholders](#-optional-placeholders)
6. [Extend Rule with Class Selector](#-extend-rule-with-class-selector)
7. [Extend Pseudo Selector](#-extend-pseudo-selector)

### &#10022; Placeholder Declaration:

Sass Placeholder can be declared by starts with percentage symbol `%` followed by placeholder name. And it contains style rule. That would not compiled into CSS until it is extended in some other style rules.

```scss
.link, %link {
  font-weight: normal;
}

%link:hover {
  font-weight: bold;
  color: red;
}
```

*Respective CSS Output:*

```css
.link {
  font-weight: normal;
}
```

### &#10022; Extending Placeholders:

Sass Placeholders and it's definitions will be utilized by `@extend` rule inside another style rule. Otherwise it would not emitted in the CSS output. 

```scss
%link {
	font-weight: normal;
	color: blue;
}

%link:hover {
	font-weight: bold;
	color: red;
}

a {
	@extend %link;	
}
```

*Respective CSS Output:*

```css
a {
  font-weight: normal;
  color: blue;
}

a:hover {
  font-weight: bold;
  color: red;
}
```

### &#10022; Extending Multiple Placeholders:

Sass can extend multiple class selectors and placeholders with comma separated.

```scss
%-link {
	border-radius: 0px;
	color: #424242;
	background-color: #F7F7F7;
	padding: 5px 10px;
}

%font {
	font-family: 'Open Sans', sans-serif;
}

.button {
	@extend %-link, %font;
}
```

*Respective CSS Output:*

```css
.button {
  border-radius: 0px;
  color: #424242;
  background-color: #F7F7F7;
  padding: 5px 10px;
}

.button {
  font-family: "Open Sans", sans-serif;
}
```

### &#10022; Private Placeholders:

Sass gives possibilities to control placeholder visibility by adding hyphen `-` or underscore `_`. It is just like a private members declaration. 

This private placeholders can be accessible and visible within the current stylesheet.

```scss
// main.scss
@use 'partials';

// _partials.scss
%-link {
	border-radius: 0px;
	color: #424242;
	background-color: #F7F7F7;
	padding: 5px 10px;
}

.button {
	@extend %-link;
}
```

*Respective CSS Output:*

```css
.button {
  border-radius: 0px;
  color: #424242;
  background-color: #F7F7F7;
  padding: 5px 10px;
}
```

See More Private Member at [Meta Comments](./meta-comments.md)

### &#10022; Optional Placeholders:

If the specific placeholder has problem with accessibility or visibility. But it required to compile without private placeholders by setting `!optional` flag at the end of it. 

```scss
@extend %link !optional;
```

### &#10022; Extend Rule with Class Selector:

`@extend` Rule can inherit or extend styles from another block or class selector or placeholder. 

```scss
.alert {
	width: 100%;
	border-radius: 10px;

  &-danger {
    @extend .alert;
	  background-color: #EF5350;
	  color: #EDEDED;
  }

  &-warning {
    @extend .alert;
	  background-color: #FFEB3B;
	  color: #424242;
  }
}
```

*Respective CSS Output:*

```css
.alert, .alert-warning, .alert-danger {
  width: 100%;
  border-radius: 10px;
}
.alert-danger {
  background-color: #EF5350;
  color: #EDEDED;
}
.alert-warning {
  background-color: #FFEB3B;
  color: #424242;
}
```

### &#10022; Extend Pseudo Selector:

`@extend` Rule can inherit styles from another block or level or placeholder as well as their pseudo style rules. 

```scss
.button {
	border-radius: 0px;
	padding: 5px 10px;
	transition: all 0.3s ease;

	&:hover {
		border-radius: 10px;
		letter-spacing: 3px;
	}

	&-danger {
		@extend .button;
	}

	&-warning {
		@extend .button;
	}
}
```

*Respective CSS Output:*

```css
.button, .button-warning, .button-danger {
  border-radius: 0px;
  padding: 5px 10px;
  transition: all 0.3s ease;
}
.button:hover, .button-warning:hover, .button-danger:hover {
  border-radius: 10px;
  letter-spacing: 3px;
}
```

---
[&#8682; To Top](#-placeholders)

[&#10094; Previous Topic](./mixins.md) &emsp; [Next Topic &#10095;](./functions.md)

[&#8962; Goto Home Page](../README.md)