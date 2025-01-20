## &#10162; Organization:

Sass provide possibilities and helps to develop projects from wide range of scale. It is essential to organize the project for maintainable and scalable project to get effective outcome of it. 

### &#9780; Overview:
1. [File Structure](#-file-structure)
2. [Import Order](#-import-order)
3. [Naming Conventions](#-naming-conventions)

### &#10022; File Structure:

- Use Sass [partials](./partials.md), to create individual partial file for different features and sections. That can be imported or included during compilation on demand.

- Modular Approach to organize similar partials and files under specific directory name. Like, `base`, `components`, `layouts` and so on.


### &#10022; Import Order:

- Import partials and other sass files in specified manner. To avoid conflict and missing error, it is recommended to import in order.

- Common Order:
	- `_variables.scss`
	- `_mixins.scss`
	- `_base.scss`	

- In above Common Order, `_mixins.scss` might use the variables, which is declared in `_variables.scss` and `_base.scss` might contains all base styles based on `_variables.scss` and `_mixins.scss`.

### &#10022; Naming Conventions:

Give meaningful and consistent names: 
- Use `$primary-color` for variable, instead of `$color1`.
- Use `@mixin border-radius` for mixin name, instead of `rounded`.

---
[&#8682; To Top](#-organization)

[&#10094; Previous Topic](./modules.md) &emsp; [Next Topic &#10095;](./performance-optimization.md)

[&#8962; Goto Home Page](../README.md)