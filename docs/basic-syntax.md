## &#10162; Basic Syntax:
This will instruct about Sass syntax and project setting up information.

### &#9780; Overview:
1. [Syntax Types](#-syntax-types)
2. [Setting up](#-setting-up)
3. [Comments](#-comments)

### &#10022; Syntax Types:
It supports two types of syntaxes.

**SCSS (Sassy CSS):**

- This follows CSS-like syntax with extensions.
- This is easier and readable.
*Example:*
```css
$primary-color: blue;

.button {
   background-color: $primary-color;
   padding: 10px 15px;
}
```

**Sass (Indented Syntax):**

- This uses indentation to define blocks.
- This is more concise and minimalistic.
*Example:*
```css
$primary-color: blue;

.button
   background-color: $primary-color
   padding: 10px 15px
```

### &#10022; Setting Up:
A typical Sass project will follow similar structure, which might look like below:
```
project/
  styles/
    _variables.scss
    _mixins.scss
    _base.scss
    main.scss
```

**For large-scale projects:**

```
project/styles/
  layout/
    _layout.scss
    _header.scss
    _footer.scss
    _sidebar.scss
  components/
    _button.scss
    _form.scss
    _card.scss
    _modal.scss
    _table.scss
  utilities/
    _utilities.scss 
  _base.scss
  _typography.scss
  _colors.scss
  _mixins.scss
  _functions.scss
  main.scss
```

- `layout` directory is place for different chunks of styles for different sections. 
	- `_layout.scss` contains overall layout styles such as grid system, containers and spacing.
	- `_header.scss` contains styles implementation for header section
	- `_footer.scss` contains styles implementation for footer section
	- `_sidebar.scss` contains styles implementation for sidebar section 

- `components` directory is place for different chunks of styles for different components. 
	- `_button.scss` contains styles for the button components might reused through out the project.
	- `_form.scss` contains styles for the form components might reused through out the project.
	- `_card.scss` contains styles for the card components might reused through out the project.
	- `_modal.scss` contains styles for the modal components might reused through out the project.
	- `_table.scss` contains styles for the table components might reused through out the project.

- `utilities` directory is place for different chunks of styles for different utilities. 
	- `_utilities.scss` contains classes for common styles like margin, padding, text alignment.

- `project/styles` directory is place for base styles and their resources. 
	- `_variables.scss` contains global variables to be used through out the project.
	- `_base.scss` contains global styles like resets, typography and color palettes.
	- `_typography.scss` contains styles including font size, line height, font families.
	- `_colors.scss` defines theme and color palettes.
	- `_mixins.scss` contains reusable mixins for common styles like border-radius, box-shadow, transitions.
	- `_functions.scss` defines custom functions.
	- `main.scss` is the root and main style file for overall project which organize all other styles and resources.

### &#10022; Comments:
Sass supports two types of comments:

**Single-line comments:**
```scss
// This is a single-line comment
```

**Multi-line comments:**
```scss
/*
This is a 
multi-line comment
*/
```

---
[&#8682; To Top](#-basic-syntax)

[&#10094; Previous Topic](./introduction.md) &emsp; [Next Topic &#10095;](./datatypes-and-variables.md)

[&#8962; Goto Home Page](../README.md)