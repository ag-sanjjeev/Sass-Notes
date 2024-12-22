## &#10162; Partials:
Partials are useful feature in Sass. That are divided into smaller stylesheet files which contain reusable styles. That partials are not compiled directly into CSS. Instead, That should be imported into other Sass files to compile and use their styles.

### &#9780; Overview:
1. [Defining Partials](#-defining-partials)
2. [Import Partials](#-import-partials)

### &#10022; Defining Partials:
Sass partials can be created with leading underscore `_` in their filename to indicate. The `_variables.scss` is identified as sass partials. Which contains reusable styles. That can be imported in another Sass stylesheet.

```scss
// _variables.scss
$background-color: #FFF;
$text-color: #000;
```

### &#10022; Import Partials:
Sass partials can be imported and reused their styles in another stylesheet using `@import` at-rule. When import partials, it is possible to leave of underscore `_`.

```scss
// main.scss
@import "variables";

body {
  background-color: $background-color;
  color: $text-color;
}
```

*Respective CSS Output:*

```css
body {
  background-color: #FFF;
  color: #000;
}
```

---
[&#8682; To Top](#-partials)

[&#10094; Previous Topic](./nesting.md) &emsp; [Next Topic &#10095;](./strings.md)

[&#8962; Goto Home Page](../README.md)