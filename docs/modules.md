## &#10162; Modules:

Sass has several built-in modules to bring useful functions to simplify the process of compiling styles. 

Sass built-in modules URL begin with `sass:` and followed by `<module-name>`.

Before sass modules comes into picture, the all other built-in functions are available globally. In later versions, that are deprecated. But it available still to support for older versions. Thus, the best practices are import respective modules to use their built-in functions. 

### &#9780; Overview:
1. [Built-in Modules](#-built-in-modules)
2. [Importing Modules](#-importing-modules)

### &#10022; Built-in Modules:

There are several built-in modules as follows: 
- `sass:color`: it provides functions to deal with colors and color based themes.
- `sass:list`: it provides functions to deal with sass lists.
- `sass:map`: it provides functions to deal with sass maps.
- `sass:math`: it provides functions that used for work with numbers.
- `sass:meta`: it used to bring detailed information about sass works.
- `sass:selector`: it provides functions to handle selectors.
- `sass:string`: it provides functions that used to manipulate strings.


### &#10022; Importing Modules:

Sass modules can be imported with at-rule called `@use` directive followed by module name. This brings all functions available under those module name to be utilized through out the stylesheet. 

This will load modules from node_modules.

*Example:*

```scss
@use 'sass:math' as math;
```

---
[&#8682; To Top](#-modules)

[&#10094; Previous Topic](./maps-and-lists.md) &emsp; [Next Topic &#10095;](./naming-conventions.md)

[&#8962; Goto Home Page](../README.md)