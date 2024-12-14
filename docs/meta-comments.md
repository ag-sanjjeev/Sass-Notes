## &#10162; Meta Comments:
Meta-comments are special feature in Sass that comments can control the Sass compilation process. Which gives various comments to customize the behavior of the compilation process without affecting output CSS.

### &#9780; Overview:
1. [At Rules](#-at-rules)
2. [Compilation Control](#-compilation-control)
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

(import, use, forward)
- `@import`: Imports other Sass partials and styles.
  ```scss
  @import "base";
  @import "layout";
  ```

- `@use`: Imports modules from Built-in Sass Node modules.
  ```scss
  @use "sass:math";
  ```

- `@forward`: Import modules with custom configuration. 

  *Usage 1:*

  ```scss
  @forward 'partials' as part-*;

  $part-color: red !default;
  ```

  *Usage 2:*

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

- `@mixin`: Defines a reusable block of CSS.
  ```scss
  @mixin border-radius($radius) {
    border-radius: $radius;
  }
  ```
  See More about [Mixins](./mixins.md)

- `@function`: Defines a reusable function.
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
- `@debug`: Outputs a message or value to the console during compilation.
  ```scss
  @debug "A debug message";
  @debug $color;
  ```

- `@warn`: Outputs a warning message during compilation.
  ```scss
  @warn "A warning message";

  @if $color == red {
    @warn "It is not recommended to use";
  }
  ```

- `@error`: Throws an error and halts the compilation process.
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

[&#10094; Previous Topic](./partials.md) &emsp; [Next Topic &#10095;](./mixins.md)

[&#8962; Goto Home Page](../README.md)