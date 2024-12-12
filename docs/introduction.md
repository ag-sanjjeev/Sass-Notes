## &#10162; Introduction:
This introduction will gives the basic information about Sass before getting into topics.

### &#9780; Overview:
1. [What is Sass?](#-what-is-sass)
2. [Installation](#-installation)
3. [Compile Sass](#-compile-sass)
4. [Need for Sass](#-need-for-sass)

### &#10022; What is Sass?:
Sass stands for Syntactically Awesome Style Sheets. It is a CSS pre-processor that compiles into CSS. It has various features like variables, nested rules, mixins, functions, and more. To make it more efficient and maintainable.

### &#10022; Installation:
Sass compiler can be installed with following package managers:
- Using Node Package Manager:
```bash
npm install -g sass
```

- Using Yarn Package Manager
```bash
yarn global add sass
```

- For easy and live compilation with IDE by installing relevant plug-ins and configure it for desired operation.

### &#10022; Compile Sass:
**Basic Usage:**

To compile `Sass` into `CSS`

```bash
sass input.scss output.css
```

**Output Style Options:**

- `Expanded`: Expands nested rules (default).
```bash
sass input.scss output.css --style=expanded
```

- `Compressed`: Minifies CSS further by removing unnecessary spaces.
```bash
sass input.scss output.min.css --style=compressed
```

**Source Maps:**

It generate source maps to help with debugging:
```bash
sass input.scss output.css --source-map
```

To opt-out source maps:
```bash
sass input.scss output.css --no-source-map
```

**Watch Mode:**

To recompile Sass files automatically, when it changed:
```bash
sass input.scss output.css --watch
```

**Specific Output Directory:**

```bash
sass style.scss dist/css/style.css
```

**Precision:**

To set precision for floating point numbers.
```bash
sass input.scss output.css --precision=6
```

**Load Path:**

To load additional directories to search for imports.
```bash
sass input.scss output.css --load-path=modules/styles/style.scss
```

**Load Directories:**

To specify additional directories to search for imported files.
```bash
sass -I styles input.scss output.css
```

**Quiet Operations:**

To suppresses non-error messages.
```bash
sass input.scss output.css --quiet
```

### &#10022; Need for Sass:
- It can add features that are not natively available in CSS.
- It promotes code maintainability, re-usability and organization.
- It speeds up development process.
- It can facilitates large-scale CSS projects.

---
[&#8682; To Top](#-introduction)

[&#10094; Previous Topic](../README.md) &emsp; [Next Topic &#10095;](./basic-syntax.md)

[&#8962; Goto Home Page](../README.md)