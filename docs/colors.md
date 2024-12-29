## &#10162; Colors:


### &#9780; Overview:
1. [HSL Color](#-hsl-color)
2. [HWB Color](#-hwb-color)

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

Supported HSL color functions:

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

---
[&#8682; To Top](#-colors)

[&#10094; Previous Topic](./strings.md) &emsp; [Next Topic &#10095;](./meta-comments.md)

[&#8962; Goto Home Page](../README.md)