## &#10162; Colors:

Sass has modules for colors. It has built-in functions to create varieties of colors and color schemes.

### &#9780; Overview:
1. [HSL Color](#-hsl-color)
2. [HWB Color](#-hwb-color)
3. [LAB Color](#-lab-color)
4. [LCH Color](#-lch-color)
5. [OKLAB Color](#-oklab-color)
6. [OKLCH Color](#-oklch-color)
7. [RGB Color](#-rgb-color)
8. [Color Adjust Function](#-color-adjust-function)

### &#10022; HSL Color:

HSL stands for Hue, Saturation and Lightness.
Where,
- `Hue` value should be a angle between 0deg and 360deg and may be unit-less as a number between 0 and 360. And the value outside than specified range will be treated to with in range by modulus operation such as $hue % 360. 
- `Saturation` value should be a percentage between 0% and 100% and may be unit-less as a number between 0 and 100. Saturation value below than 0% then it will be clamped to 0%. But above 100% will be allowed to represent that, it is out of standard RGB color.
- `Lightness` value should be a percentage between 0% and 100% and may be unit-less as a number between 0 and 100. Lightness value out of range on both lower and upper limit are allowed to represent that, it is out of standard RGB color.
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.

Supported HSL color functions:

**HSL color function:**

```scss
$hue: 120deg;
$saturation: 50%;
$lightness: 60%;
$alpha: 0.5;

@debug hsl($hue $saturation $lightness);
@debug hsl($hue, $saturation, $lightness, $alpha: 1);
```

*Respective Compilation Message:*

```bash
test\main.scss:6 DEBUG: hsl(120deg, 50%, 60%)
test\main.scss:7 DEBUG: hsl(120deg, 50%, 60%)
```

**HSL with alpha channel color function:**

```scss
@debug hsla($hue $saturation $lightness);
@debug hsla($hue, $saturation, $lightness, $alpha: 1);
```

*Respective Compilation Message:*

```bash
test\main.scss:8 DEBUG: hsl(120deg, 50%, 60%)
test\main.scss:9 DEBUG: hsl(120deg, 50%, 60%)
```

### &#10022; HWB Color:

HWB stands for Hue, Whiteness and Blackness.

Where,
- `Hue` value should be a angle between 0deg and 360deg and may be unit-less as a number between 0 and 360. And the value outside than specified range will be treated to with in range by modulus operation such as $hue % 360. 
- `Whiteness` value should be a percentage between 0% and 100% and without percentage is not allowed.
- `Blackness` value should be a percentage between 0% and 100% and without percentage is not allowed.
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.
- The total value of both `Whiteness` and `Blackness` are should be under 100%. If exceeds above the 100% then scaled to be 100%. If it is below 0% then it is treated as out of standard RGB color.

`color.hwb()` function is deprecated. Use the global `hwb()` function instead.

Supported HWB color functions:

```scss
@use 'sass:color';

$hue: 120deg;
$whiteness: 50%;
$blackness: 60%;
$alpha: 0.5;

@debug hwb($hue $whiteness $blackness);
@debug hwb($hue $whiteness $blackness $alpha);
@debug color.hwb($hue $whiteness $blackness);
@debug color.hwb($hue, $whiteness, $blackness, $alpha: 1);
```

*Respective Compilation Message:*

```bash
test\main.scss:8 DEBUG: hwb(120deg 50% 60%)
test\main.scss:9 DEBUG: hwb(120deg 50% 60% 0.5)
test\main.scss:10 DEBUG: #747474
test\main.scss:11 DEBUG: #747474
```

### &#10022; LAB Color:

LAB stands for Lightness, A and B.

Where,
- `Lightness` value should be a percentage between 0% and 100% and may be unit-less as a number between 0 and 100. And the value outside than specified range will be treated to clamped with in the range. 
- `a` channel value should be a percentage between -100% and 100% and may be a number ranges between -125 and 125. If it is out of range then it represents a color outside the standard CIELAB.
- `b` channel value should be a percentage between -100% and 100% and may be a number ranges between -125 and 125. If it is out of range then it represents a color outside the standard CIELAB.
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.

Supported LAB color functions:

```scss
lab($lightness $a $b);
lab($lightness $a $b, $alpha);
```

*Example:*

```scss
$lightness: 50%;
$a: 30%;
$b: -15;
$alpha: 0.5;

@debug lab($lightness $a $b);
@debug lab($lightness $a $b, $alpha);
```

*Respective Compilation Message:*

```css
test\main.scss:6 DEBUG: lab(50% 30% -15)
test\main.scss:7 DEBUG: lab(50% 30% -15, 0.5)
```

### &#10022; LCH Color:

LCH stands for Lightness, Chroma and Hue.

Where,
- `Lightness` value should be a percentage between 0% and 100% and may be unit-less as a number between 0 and 100. And the value outside than specified range will be treated to clamped with in the range. 
- `Chroma` channel value should be a percentage between 0% and 100% and may be a number ranges between 0 and 150. If it is below lowest value, that will be clamped to 0 or 0%. If it exceeds the upper limit then it represents a color outside the standard CIELAB.
- `Hue` value should be a angle between 0deg and 360deg and may be unit-less as a number between 0 and 360. And the value outside than specified range will be treated to with in range by modulus operation such as $hue % 360. 
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.

Supported LCH color functions:

```scss
lch($lightness $chroma $hue);
lch($lightness $chroma $hue, $alpha);
```

*Example:*

```scss
$lightness: 75%;
$chroma: 10;
$hue: 150deg;
$hue2: 0.3turn;
$alpha: 0.5;

@debug lch($lightness $chroma $hue);
@debug lch($lightness $chroma $hue2, $alpha);
```

*Respective Compilation Message:*

```bash
test\main.scss:7 DEBUG: lch(75% 10 150deg)
test\main.scss:8 DEBUG: lch(75% 10 0.3turn, 0.5)
```

### &#10022; OKLAB Color:

OKLAB similar to `LAB`, then LAB stands for Lightness, A and B. It gives perceptually-uniform lightness color with given dual channel value.

Where,
- `Lightness` value should be a percentage between 0% and 100% and may be unit-less as a number between 0 and 100. And the value outside than specified range will be treated to clamped with in the range. 
- `a` channel value should be a percentage between -100% and 100% and may be a number ranges between -0.4 and 0.4. If it is out of range then it represents a color outside the standard Oklab.
- `b` channel value should be a percentage between -100% and 100% and may be a number ranges between -0.4 and 0.4. If it is out of range then it represents a color outside the standard Oklab.
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.

Supported OKLAB color functions:

```scss
oklab($lightness $a $b)
oklab($lightness $a $b, $alpha)
```

*Example:*

```scss
$lightness: 50%;
$a: -0.2;
$b: 30%;
$alpha: 0.5;

@debug oklab($lightness $a $b);
@debug oklab($lightness $a $b,$alpha);
```

*Respective Compilation Message:*

```css
test\main.scss:6 DEBUG: oklab(50% -0.2 30%)
test\main.scss:7 DEBUG: oklab(50% -0.2 30%, 0.5)
```

### &#10022; OKLCH Color:

OKLCH similar to `LCH`, then LCH stands for Lightness, Chroma and Hue. It gives perceptually-uniform lightness color with given Chroma and Hue channel value.

Where,
- `Lightness` value should be a percentage between 0% and 100% and may be unit-less as a number between 0 and 100. And the value outside than specified range will be treated to clamped with in the range. 
- `Chroma` channel value should be a percentage between 0% and 100% and may be a number ranges between 0 and 0.4. If it is below lowest value, that will be clamped to 0 or 0%. If it exceeds the upper limit then it represents a color outside the standard Oklab.
- `Hue` value should be a angle between 0deg and 360deg and may be unit-less as a number between 0 and 360. And the value outside than specified range will be treated to with in range by modulus operation such as $hue % 360. 
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.

Supported OKLCH color functions:

```scss
oklch($lightness $chroma $hue);
oklch($lightness $chroma $hue, $alpha);
```

*Example:*

```scss
$lightness: 50%;
$chroma: 0.1;
$hue: 60deg;
$hue2: 0.3turn;
$alpha: 0.5;

@debug oklch($lightness $chroma $hue);
@debug oklch($lightness $chroma $hue2, $alpha);
```

*Respective Compilation Message:*

```bash
test\main.scss:7 DEBUG: oklch(50% 0.1 60deg)
test\main.scss:8 DEBUG: oklch(50% 0.1 0.3turn, 0.5)
```

### &#10022; RGB Color:

RGB stands for Red, Green and Blue. It creates color based on these three color values.

Where,
- `RED` value ranges between 0 and 255 or ranges between 0% and 100%. If the channel value exceed the range then it will represents a color outside standard RGB color.
- `GREEN` value ranges between 0 and 255 or ranges between 0% and 100%. If the channel value exceed the range then it will represents a color outside standard RGB color.
- `BLUE` value ranges between 0 and 255 or ranges between 0% and 100%. If the channel value exceed the range then it will represents a color outside standard RGB color.
- `Alpha` channel value should be within 0 and 1 and may be a percentage between 0% and 100%.

Supported RGB color functions:

```scss
rgb($red, $green, $blue);
rgb($red, $green, $blue, $alpha);
rgba($red, $green, $blue, $alpha);
rgba($color, $alpha);
```

*Example:*

```scss
$red: 15;
$green: 65.3%;
$blue: 210;
$color: #F3C355;
$alpha: 0.5;
$alpha2: 60%;

@debug rgb($red $green $blue); 
@debug rgb($red, $green, $blue, $alpha); 
@debug rgb($color, $alpha);
@debug rgba($red, $green, $blue, $alpha); 
@debug rgba($color, $alpha);
@debug rgba(rgba($red, $green, $blue, $alpha), 1);
```

*Respective Compilation Message:*

```bash
test\main.scss:8 DEBUG: rgb(15, 167, 210)
test\main.scss:9 DEBUG: rgba(15, 167, 210, 0.5)
test\main.scss:10 DEBUG: rgba(243, 195, 85, 0.5)
test\main.scss:11 DEBUG: rgba(15, 167, 210, 0.5)
test\main.scss:12 DEBUG: rgba(243, 195, 85, 0.5)
test\main.scss:13 DEBUG: #0fa7d2
```

### &#10022; Color Adjust Function:

Color adjust function is used to adjust any of the channels for the given color. It gives possibility to adjust `red`, `green`, `blue`, `hue`, `saturation`, `lightness`, `whiteness`, `blackness`, `x`, `y`, `z`, `chroma`, `alpha` and `space` channels. 

But it requires the color in the first argument. To adjust any particular channel for given color, then need to specify their key value pair alone.

All the channel values will accepts and clamped to their desired range of limit based on space channel provided.

```scss
color.adjust($color,
  $red: null, $green: null, $blue: null,
  $hue: null, $saturation: null, $lightness: null,
  $whiteness: null, $blackness: null,
  $x: null, $y: null, $z: null,
  $chroma: null,
  $alpha: null,
  $space: null);
```

---
[&#8682; To Top](#-colors)

[&#10094; Previous Topic](./strings.md) &emsp; [Next Topic &#10095;](./meta-comments.md)

[&#8962; Goto Home Page](../README.md)