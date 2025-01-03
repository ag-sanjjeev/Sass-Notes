## &#10162; Meta Comments:
Meta-comments are special feature in Sass that comments can control the Sass compilation process. Which gives various comments to customize the behavior of the compilation process without affecting output CSS.

### &#9780; Overview:
1. [At Rules](#-at-rules)
2. [Compilation Control](#-compilation-control)
    - [Import](#-import)
    - [Use](#-use)
    - [Forward](#-forward)
    - [Mixin](#-mixin)
    - [Function](#-function)
3. [Conditional Compilation](#-conditional-compilation) 
4. [Debugging and Error Handling](#-debugging-and-error-handling) 

### &#10022; At Rules:
At-rules are directives that starts with `@` symbol which control the behavior and flow of the Sass compilation process.

**Common At-Rules:**
- `@at-root`,
- `@debug`,
- `@each`,
- `@else`,
- `@else if`,
- `@error`,
- `@extend`,
- `@for`,
- `@forward`,
- `@function`,
- `@if`,
- `@import`,
- `@include`,
- `@mixin`,
- `@use`,
- `@warn`

### &#10022; Compilation Control:
These meta-comments defines the compilation flow by adding external styles before compile styles.

List of common compilation control:
- [Import](#-import),
- [Use](#-use),
- [Forward](#-forward),
- [Mixin](#-mixin),
- [Function](#-function),

### &#10022; Import: 

Imports other Sass modules, partials and styles. It can import Sass files and CSS styles. It is not like CSS imports. But it requires a browser to make HTTP request as it renders the page. 

Sass imports are always handle during compilation. It is same as CSS import except it will allow multiple imports on each @import statement.

Indented Sass doesn't require quoted string for the URL in the import.

Import statement might going to be `deprecated`. But it is preferred to use `@use` rule instead.

```scss
@import "theme.css";
@import "base";
@import url(layout);
@import "https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&display=swap";
@import "landscape" screen and (orientation: landscape);
```

**Interpolation:**

It can possible to dynamically import through plain CSS import with mixins and functions. But Sass can't directly offer to interpolate imports.

```scss
// _variables.scss
@mixin import-font($family) {
  @import url("http://fonts.googleapis.com/css2?family=#{$family}");
}

// main.scss
@use 'variables';
@include variables.import-font('Open+Sans');
```

*Respective CSS Output:*

```css
@import url("http://fonts.googleapis.com/css2?family=Open+Sans");
```

**Problems with Import Statement:**
- @import will make all members are globally accessible. So, it necessary and require to add prefix to make them unique and avoid conflict with others on large scale projects.
- @extend rule also make all members are globally accessible. And it is difficult to identify which module gets extended.
- It will compile Sass styles and exports the respective CSS each time when @import statement found in the Sass stylesheet. So, it increases the compilation time and exports bloated CSS output.
- It is not possible to define private members or no way to control visibility to it's members.

### &#10022; Use: 

Imports modules from Built-in Sass Node modules. Imports other Sass styles such as mixins, functions, etc., It also imports styles from external URL.

Each @use rule loads one file at once. and it can have have only one URL.

@use rule must requires quotes around file names and URLs, eventhough the indented syntax.

@use rules must declared at top of any other rules except @forward and style rules. But it be used after variables declaration when need for configuring modules. And it cannot be nested in style rules.

@use rule can find modules with different supported extension. If  `@use 'variables';` declared then it looks for `_variables.scss`, `_variables.sass`, or `variables.css`. Thus, it can load compiled CSS as well.

```scss
@use "sass:math";
@use "http://localhost/styles/_variables.sass";
```

**Loading Members:** 

with @use rule to access members of Sass styles such as functions, mixins and variables by @include rule. `@include <namespace>.<member>`

```scss
// _mixins.scss
@mixin shadow {
  box-shadow: 5px 5px 10px 0px rgba(121, 85, 72, 0.3);
}

// main.scss
@use 'mixins';

.card {
  background-color: #FFF;
  @include mixins.shadow;
}
```

*Respective CSS Output:*

```css
.card {
  background-color: #FFF;
  box-shadow: 5px 5px 10px 0px rgba(121, 85, 72, 0.3);
}
```

**Permalink:** 

When access long and lengthy styles filename in shorter with @use rule and `as` keyword. 

```scss
@use 'mixins' as m;

.card {
  @include m.shadow;
}
```

*Without Namespace* to load module with asterisk `*`.

```scss
@use 'mixins' as *;

.card {
  @include shadow;
}
```

**Private Members:**

It prevent certain members of a namespace modules to be accessed outside. By declaring them starts with hyphen `-` or underscore `_`. This applies to mixins, functions and variables like `@mixin -mxname`, `@function -fnname()`.

```scss
// _mixins.scss
// private member
$-shadowColor: rgba(121, 85, 72, 0.3);
@mixin shadow {
  box-shadow: 5px 5px 10px 0px $-shadowColor;
}

// main.scss
@use 'mixins';

.card {
  background-color: #FFF;
  @include mixins.shadow;

  // throws an error
  color: mixins.$-shadowColor;
}
``` 

**Respective Compilation Message:**

```bash
Error: Private members can't be accessed from outside their modules.
  ╷
9 │     color: mixins.$-shadowColor;
  │            ^^^^^^^^^^^^^^^^^^^^
  ╵
  test\main.scss 9:12  root stylesheet
```

**Configuration:** 

To define variables with `!default` flag to configure outside.

```scss
// _mixins.scss
// public member can be configured
$shadowColor: rgba(121, 85, 72, 0.3) !default;
@mixin shadow {
  box-shadow: 5px 5px 10px 0px $shadowColor;
}

// main.scss
@use 'mixins' with (
  $shadowColor: rgba(150, 85, 75, 0.1)
);

.card {
  background-color: #FFF;
  @include mixins.shadow;
}
```

*Respective CSS Output:*

```css
.card {
  background-color: #FFF;
  box-shadow: 5px 5px 10px 0px rgba(150, 85, 75, 0.1);
}
```

**Overwriting Variables:** 

To reassign value to existing variables by creating separate overwrite Sass styles. But built-in modules' variable can't be overwritten.

```scss
// _variables.scss
$primary: blue;

// _overwrite.scss
@use 'variables';
variables.$primary: green; 

// main.scss
@use 'variables';
@use 'overwrite';

@debug variables.$primary;
```

*Respective Compilation Message:*

```bash
test\main.scss:6 DEBUG: green
```

**Overwriting a built-in modules' variables:**

Sass prevents overwrite to an existing modules' variables. 

```scss
@use 'sass:math';

// overwriting built-in variable
math.$pi: 3.14;

@debug math.$pi;
```

*Respective Compilation Message:*

```bash
Error: Cannot modify built-in variable.
╷
4 │   math.$pi: 3.14;
│   ^^^^^^^^^^^^^^
╵
test\main.scss 4:3  root stylesheet
```

### &#10022; Forward: 

@forward rule is similar to @use rule in Sass. It loads functions, mixins and variables from other stylesheets. It make public members to be available in the current stylesheet. 

Each @forward rule loads one file at once. and it can have have only one URL.

@forward rule must requires quotes around file names and URLs, eventhough the indented syntax.

It is suggested and good practices to write @forward rule first before @use rule for same Sass stylesheet. Because, configuration will be applied first with the @forward rule before any @use rule takes place to load without configuration.

@forward rule can be extended with @use rule, eventhough not yet used.

It import modules as same as @use rule with custom configuration on it. 

**Usage 1:**

```scss
@forward 'partials' as part-*;

$part-color: red !default;
```

**Usage 2:**

```scss
// _base.scss
$white: #FFFFFF !default;
$black: #000000 !default;
$border-radius: 15px !default;
$box-shadow: 0 5px 5px rgba($black, 0.1) !default;

.card {
  background-color: $white;
  color: $black;
  border-radius: $border-radius;
  box-shadow: $box-shadow;
}

// _cards.scss
@forward 'base' with (
  $black: #1B1B1B !default,
  $border-radius: 10px !default
);

// main.scss
@use 'cards' with ($white: #E7E7E7);
```

*Respective CSS Output:*

```css
.card {
  background-color: #E7E7E7;
  color: #1B1B1B;
  border-radius: 10px;
  box-shadow: 0 5px 5px rgba(27, 27, 27, 0.1);
}
```

**Extending @forward rule:**

```scss
// _resets.scss
@mixin list-reset {
  margin: 0;
  padding: 0;
  list-style: none;
}

// _partials.scss
@forward "resets";

// styles.scss
@use "partials";

li {
  @include partials.list-reset;
}
```

*Respective CSS Output:*

```css
li {
  margin: 0;
  padding: 0;
  list-style: none;
}
```

**Adding Prefix:**

Module members are used with namespace. Their names might make no sense when it declared simple and short. Add prefix to all of their members for identification. It is possible to add prefix with @forward rule.

```scss
// _links.scss
@mixin reset {
  margin: 0;
  padding: 0;
  text-decoration: none;
}

// _partials.scss
@forward "links" as links-*;

// main.scss
@use "partials";

a {
  @include partials.links-reset;
}
``` 

*Respective CSS Output:*

```css
a {
  margin: 0;
  padding: 0;
  text-decoration: none;
}
```

**Controlling Visibility:**

To make some members to kept as private and don't allow them to be forwarded in further or restrict the visibility out of the module. It is possible to control visibility of the member with keywords `show` and `hide`.

```scss
// _links.scss
$font-weight: bold;

@mixin reset {
  margin: 0;
  padding: 0;
  text-decoration: none;
}

@mixin anchor-links {
  @include reset;

  font-weight: $font-weight;
}

// _partials.scss
@forward "links" hide reset, $font-weight;

// main.scss
@use "partials";

a {
  @include partials.anchor-links;
}
```

*Respective CSS Output:*

```css
a {
  margin: 0;
  padding: 0;
  text-decoration: none;
  font-weight: bold;
}
```

### &#10022; Mixin: 

Defines a reusable block of CSS.

```scss
@mixin border-radius($radius) {
  border-radius: $radius;
}
```
See More about [Mixins](./mixins.md)

### &#10022; Function: 

Defines a reusable function.

```scss
@use 'sass:math';
@function rem($pixel) {
  @return math.div($pixel, 16) + rem;
}
```
See More about [Functions](./functions.md)

### &#10022; Conditional Compilation:
- `@if`, `@else`, `@else if`: Conditional statements.
  
- `@for`: Iterative loop.  

- `@each`: Iterates over a list or map.

  See More about [Control Flow Statements](./control-directives.md)

### &#10022; Debugging and Error Handling:
- `@debug`: 

  Outputs a message or value to the console during compilation.

  ```scss
  @debug "A debug message";
  @debug $color;
  ```

- `@warn`: 

  Outputs a warning message during compilation.

  ```scss
  @warn "A warning message";

  @if $color == red {
    @warn "It is not recommended to use";
  }
  ```

- `@error`: 

  Throws an error and halts the compilation process.

  ```scss
  @use 'sass:math';

  @function pixel2rem($pixel) {
    @if type-of($pixel) != 'number' {
      @error "pixel should be a number";
    } 
    @return math.div($pixel, 16) + rem;
  }

  p {
    font-size: pixel2rem(intial);
  }
  ```

  *Respective CSS Output:*

  ```css
    Error: "pixel should be a number"
     ╷
  11 │     font-size: pixel2rem(intial);
     │                ^^^^^^^^^^^^^^^^^
     ╵
    test\main.scss 11:13  root stylesheet
  ```

---
[&#8682; To Top](#-meta-comments)

[&#10094; Previous Topic](./colors.md) &emsp; [Next Topic &#10095;](./mixins.md)

[&#8962; Goto Home Page](../README.md)