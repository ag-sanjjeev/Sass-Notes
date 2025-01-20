## &#10162; Performance Optimization:

It is important for large set of projects, which significantly improve performance of overall compilation and styles.

### &#9780; Overview:
1. [Minimize File Size](#-minimize-file-size)
2. [Optimize Calculations](#-optimize-calculations)
3. [Minimize Control Directive](#-minimize-control-directive)
4. [Utilize Sass Modules](#-utilize-sass-modules)

### &#10022; Minimize File Size:

File size will affect overall performance of the sass project. Consider following practices to improve performance. 

- Reduce Unnecessary Nesting which will increase the compiled CSS file size.
- Use Partials, Break down large styles into smaller partials to import and include on demand to reduce file size.
- Remove Unused Code: Review and remove unused styles or variables.

### &#10022; Optimize Calculations:

- Avoid Complex Calculations within Sass code. Which will slow down compilation.
- Use Built-in Functions for color manipulation, math operations and string related manipulation whenever possible.


### &#10022; Minimize Control Directive:

- Avoid unnecessary control statements and use it effectively.
- Optimize Loops and avoid unnecessary iterations.


### &#10022; Utilize Sass Modules:

- Import specific modules only. That are required and actually used in a specific file.
- Use the `as` keyword to create aliases. Which will improve readability and reduce the risk of naming conflicts.

---
[&#8682; To Top](#-performance-optimization)

[&#10094; Previous Topic](./organization.md) &emsp; [Next Topic &#10095;](./css-methodology.md)

[&#8962; Goto Home Page](../README.md)