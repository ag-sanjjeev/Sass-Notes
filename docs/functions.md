## &#10162; Functions:
Sass provides function feature like programmatic approach to the CSS styles. Which gives possibilities to use built-in functions available in Sass as well as define custom one.

Sass function might accept arguments and return values.

Sass allow to define and perform complex operations on values that you can be used throughout the stylesheet.

Sass function name doesn't begin with double hyphens `--`. Sass function treats both hyphens `-` and underscore `_` in their name.

Sass can possible to manipulate global values. But it is not recommended in functions to manipulate or affect the global value. Sass functions recommended to use for performing calculations. Use mixins to affect and manipulate global value.

Sass function can accepts arguments both positional arguments and named or keyword arguments values like [mixins](./mixins.md).

Sass function can accepts arbitrary arguments like [mixins](./mixins.md#-arbitrary-keyword).

### &#9780; Overview:
1. [Function Declaration](#-function-declaration)
2. [Function Call](#-function-call)
3. [Function Arguments](#-function-arguments)
4. [Built-in Functions](#-built-in-functions)

### &#10022; Function Declaration:

Custom Sass functions can be declared by starts with `@function` rule followed by function name. That function name should be a standard naming conventions followed by Sass.

```scss
@use "sass:math";

@function pixel2rem($px) {
  @return math.div($px,16) + rem;
}
```

### &#10022; Function Call:

```scss
h1 {
  font-size: pixel2rem(16);
}
```

*Respective CSS Output:*

```css
h1 {
  font-size: 1rem;
}
```

### &#10022; Function Arguments:

Sass Function arguments can accept multiple arguments and it may have ___trailing commas___ to avoid errors when refactoring stylesheet.

Optionally, it may have default value argument or optional value argument. But default value argument can be declared with `argument name` followed by colon `:` and value.

*Function without trailing commas:*

```scss
@function sum($value1, $value2) {
  $sum: $value1 + $value2;
  @return $sum;
}

@debug sum(1,2);
```

*Function with trailing commas:*

```scss
@function sum($value1, $value2,) {
  $sum: $value1 + $value2;
  @return $sum;
}

@debug sum(1,2);
```

*Respective Compilation Message:*

Note: That both function definitions will give same output.

```bash
test\main.scss:8 DEBUG: 3
```

### &#10022; Built-in Functions:
Sass has varieties of built-in functions to be utilized for manipulate and to handle colors, lists, numbers and strings.

- **Color Functions:**
  - `adjust-hue($color, $degrees)`: Adjusts the hue of a color.
  - `change-color($color, $red: null, $green: null, $blue: null, $hue: null, $saturation: null, $lightness: null)`: Changes the color components.
  - `complement($color)`: Returns the complementary color.
  - `darken($color, $amount)`: Darkens a color.
  - `desaturate($color, $amount)`: Desaturates a color.
  - `grayscale($color)`: Converts a color to grayscale.
  - `invert($color)`: Inverts the color.
  - `lighten($color, $amount)`: Lightens a color.
  - `mix($color1, $color2, $weight)`: Mixes two colors.
  - `red($color)`: Returns the red component of a color.
  - `green($color)`: Returns the green component of a color.
  - `blue($color)`: Returns the blue component of a color.
  - `hue($color)`: Returns the hue of a color.
  - `saturation($color)`: Returns the saturation of a color.
  - `lightness($color)`: Returns the lightness of a color.
  - `rgba($red, $green, $blue, $alpha)`: Creates an RGBA color.
  - `hsla($hue, $saturation, $lightness, $alpha)`: Creates an HSLA color.
  - `hsl($hue, $saturation, $lightness)`: Creates an HSL color.
  - `scale-color($redcolor, $lightness: +40%)`: Returns the lightness of a color.
  - `opacify(rgba(#F23, 0.5), $amount)`: Add opacity to fixed amount to the alpha channel color.
- **String Functions:**
  - `str-index($string, $find)`: Returns the index of a substring within a string.
  - `str-insert($string, $toInsert, $index)`: Inserts a string at a specific index.
  - `str-length($string)`: Returns the length of a string.
  - `str-slice($string, $start-index, $end-index)`: Extracts a substring from a string.
  - `to-lower-case($string)`: Converts a string to lowercase.
  - `to-upper-case($string)`: Converts a string to uppercase.
  - `unquote($string)`: Removes quotes from a string.
  - `quote($string)`: Adds quotes to a string.
  - See More about [String](./strings.md)
- **List Functions:**
  - `length($list)`: Returns the number of items in a list.
  - `nth($list, $n)`: Returns the nth item in a list.
  - `join($list1, $list2, ...)`: Joins multiple lists.
  - `append($list, $value)`: Appends a value to the end of a list.
  - `zip($list1, $list2, ...)`: Creates a list of tuples from multiple lists.
  - See More about [Lists](./maps-and-lists.md)
- **Map Functions:**
  - `map-get($map, $key)`: Gets the value associated with a key in a map.
  - `map-has-key($map, $key)`: Checks if a map contains a specific key.
  - `map-merge($map1, $map2, ...)`: Merges multiple maps.
  - See More about [Maps](./maps-and-lists.md)
- **Math Functions:**
  - `abs($number)`: Returns the absolute value of a number.
  - `ceil($number)`: Rounds a number up to the nearest integer.
  - `floor($number)`: Rounds a number down to the nearest integer.
  - `max($number1, $number2, ...)`: Returns the maximum value.
  - `min($number1, $number2, ...)`: Returns the minimum value.
  - `percentage($number)`: Converts a number to a percentage.
  - `random()` Returns a random number between 0 and 1 or from specified integer limit.
  - `round($number)`: Rounds a number to the nearest integer.
  - See More about [Sass Math](./sass-math.md)

**Colors Related Functions:**

```scss
// colors.scss
$redcolor: #EF5350;
$greencolor: #009688;
$bluecolor: #FFEE58;
$blackcolor: #4E342E;
$whitecolor: #F5F5F5;
$color: $redcolor;
$degrees: 180deg;
$amount: 50%;
$weight: $amount;
$alpha: $amount;

@debug "Adjusted hue:"adjust-hue($redcolor, $degrees);
@debug "Changed Color:"change-color($color, $hue: hue($color) + 180);
@debug "Complement:"complement($color);
@debug "Darken:"darken($color, $amount);
@debug "Saturate:"saturate($color, $amount);
@debug "Desaturate:"desaturate($color, $amount);
@debug "Grayscale:"grayscale($color);
@debug "Invert:"invert($color);
@debug "Lighten:"lighten($color, $amount);
@debug "Mix:"mix($redcolor, $bluecolor, $weight);
@debug "Red Component:"red($color);
@debug "Green Component:"green($color);
@debug "Blue Component:"blue($color);
@debug "Hue Component:"hue($color);
@debug "Saturation Component:"saturation($color);
@debug "Lightness Component:"lightness($color);
@debug "RGB:"rgb(123, 212, 50);
@debug "RGBA:"rgba(123, 212, 50, $alpha);
@debug "HSLA:"hsla(10deg, 83%, 35%, $alpha);
@debug "HSL:"hsl(10deg, 83%, 35%);
@debug "Scale Color:"scale-color($redcolor, $lightness: +40%);
@debug "Opacity Adjusted Color:"opacify(rgba(#F23, 0.5), 0.35);
```

*Respective Compilation Message:*

```bash
test\colors.scss:14 DEBUG: "Adjusted hue:" #50ecef
test\colors.scss:15 DEBUG: "Changed Color:" #50ecef
test\colors.scss:16 DEBUG: "Complement:" #50ecef
test\colors.scss:17 DEBUG: "Darken:" #3b0605
test\colors.scss:18 DEBUG: "Saturate:" #ff4440
test\colors.scss:19 DEBUG: "Desaturate:" #bf8180
test\colors.scss:20 DEBUG: "Grayscale:" #a0a0a0
test\colors.scss:21 DEBUG: "Invert:" #10acaf
test\colors.scss:22 DEBUG: "Lighten:" white
test\colors.scss:23 DEBUG: "Mix:" #f7a154
test\colors.scss:24 DEBUG: "Red Component:" 239
test\colors.scss:25 DEBUG: "Green Component:" 83
test\colors.scss:26 DEBUG: "Blue Component:" 80
test\colors.scss:27 DEBUG: "Hue Component:" 1.1320754717deg
test\colors.scss:28 DEBUG: "Saturation Component:" 83.2460732984%
test\colors.scss:29 DEBUG: "Lightness Component:" 62.5490196078%
test\colors.scss:30 DEBUG: "RGB:" rgb(123, 212, 50)
test\colors.scss:31 DEBUG: "RGBA:" rgba(123, 212, 50, 0.5)
test\colors.scss:32 DEBUG: "HSLA:" hsla(10deg, 83%, 35%, 0.5)
test\colors.scss:33 DEBUG: "HSL:" hsl(10deg, 83%, 35%)
test\colors.scss:34 DEBUG: "Scale Color:" DEBUG: #af1310
test\colors.scss:35 DEBUG: "Opacity Adjusted Color:" DEBUG: rgba(255, 34, 51, 0.85)
```

**List Related Functions:**

```scss
$redcolor: #EF5350;
$greencolor: #009688;
$bluecolor: #FFEE58;
$blackcolor: #4E342E;
$whitecolor: #F5F5F5;
$yellowcolor: yellow;

$list: $redcolor $greencolor $bluecolor;
$list2: $blackcolor $whitecolor;

@debug "Length:" length($list);
@debug "Nth item:" nth($list, 2);
@debug "Join List:" join($list, $list2);
@debug "Append item:" append($list, $yellowcolor);
@debug "lists into tuple by zip:" zip($list, $list2);
```

*Respective Compilation Message:*

```bash
test\main.scss:11 DEBUG: "Length:" 3
test\main.scss:12 DEBUG: "Nth item:" #009688
test\main.scss:13 DEBUG: "Join List:" (#EF5350 #009688 #FFEE58 #4E342E #F5F5F5)
test\main.scss:14 DEBUG: "Append item:" (#EF5350 #009688 #FFEE58 yellow)
test\main.scss:15 DEBUG: "lists into tuple by zip:" (#EF5350 #4E342E, #009688 #F5F5F5)
```

**Map Related Functions:**

```scss
$font-weights: ("light": 300, "normal": 400, "bold": 700);
$another-font-weights: ("thin":200, "bolder": 800);
$key: "light";

@debug "Get value for the key:" map-get($font-weights, $key);
@debug "Check key exist in the map:" map-has-key($font-weights, $key);
@debug "Merged Map:" map-merge($font-weights, $another-font-weights);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: "Get value for the key:" 300
test\main.scss:6 DEBUG: "Check key exist in the map:" true
test\main.scss:7 DEBUG: "Merged Map:" ("light": 300, "normal": 400, "bold": 700, "thin": 200, "bolder": 800)
```

**Math Related Functions:**

```scss
// main.scss
$number: 53.68;
$n1: 1.23;
$n2: -23.56;
$n3: 15;
$n4: 30.00;
$n5: 0.53;

@debug "Absoulte value:" abs($n2);
@debug "Ceiling value:" ceil($number);
@debug "Floor value:" floor($number);
@debug "Maximum value:" max($n1,$n2,$n3,$n4);
@debug "Minimum value:" min($n1,$n2,$n3,$n4);
@debug "Percentage value:" percentage($n5);
@debug "Random value null limit:" random($limit:null);
@debug "Random value:" random($limit:100);
@debug "Round value:" round($n1);
```

*Respective Compilation Message:*

```bash
test\main.scss:8 DEBUG: "Absoulte value:" 23.56
test\main.scss:9 DEBUG: "Ceiling value:" 54
test\main.scss:10 DEBUG: "Floor value:" 53
test\main.scss:11 DEBUG: "Maximum value:" 30
test\main.scss:12 DEBUG: "Minimum value:" -23.56
test\main.scss:13 DEBUG: "Percentage value:" 53%
test\main.scss:14 DEBUG: "Random value null limit:" 0.2556677392
test\main.scss:15 DEBUG: "Random value:" 59
test\main.scss:16 DEBUG: "Round value:" 1
```


---
[&#8682; To Top](#-functions)

[&#10094; Previous Topic](./placeholders.md) &emsp; [Next Topic &#10095;](./control-directives.md)

[&#8962; Goto Home Page](../README.md)