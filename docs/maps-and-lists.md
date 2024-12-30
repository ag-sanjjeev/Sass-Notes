## &#10162; Maps and List:

Maps and Lists are important concepts in Sass. It can holds series and sequence of values with different data types.

### &#9780; Overview:
1. [Maps](#-maps)
2. [Accessing Map Items](#-accessing-map-items)
3. [Add Map Items](#-add-map-items)
4. [Merging Maps](#-merging-maps)
5. [Update Map Value](#-update-map-value)
6. [Maps Deep Merge](#-maps-deep-merge)
7. [Map Remove](#-map-remove)
8. [Map Deep Remove](#-map-deep-remove)
9. [Check Map Key Exist](#-check-map-key-exist)
10. [Get Map Keys](#-get-map-keys)
11. [Get Map Values](#-get-map-values)
12. [Lists](#-lists)
13. [List Indexes](#-list-indexes)
14. [Accessing List Length](#-accessing-list-length)
15. [Identifying List Separator](#-identifying-list-separator)
16. [Accessing List Item](#-accessing-list-item)
17. [Update List Item](#-update-list-item)
18. [Get Slash Separated List](#-get-slash-separated-list)
19. [Iterating List Items](#-iterating-list-items)
20. [Append List Item](#-append-list-item)
21. [Join List Items](#-join-list-items)
22. [Zip Multiple Lists](#-zip-multiple-lists)
23. [Find List Item Index](#-find-list-item-index)
24. [Argument List](#-argument-list)
25. [List Bracketed Function](#-list-bracketed-function)

### &#10022; Maps:

Sass Maps hold keys and values pairs. It is similar to list but differs in their naming index as known as corresponding key. 

Map items are separated by commas. and key and value pair denoted as `<key> : <value>`.

The keys must be unique in map. But the values might be anything. It is recommended and good practice to use quoted string for key rather than unquoted key. 

Unlike lists, Sass map items should be wrapped around with parentheses. An empty map with no pairs can be written as `()`.

An empty map and an empty list are treated as same.


### &#10022; Accessing Map Items:

Map item value can be accessed with built-in function called `map.get()`. the first argument accepts map and last argument accepts key.

If map does not contains a key that will return `null`. It is treated as `false` or equivalent to boolean `false` to use with control flow directives.

```scss
@use 'sass:map';

$colors: ('primary': blue, 'success': green, 'danger': red);

@debug map.get($colors, 'primary');
@debug map.get($colors, 'secondary');
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: blue
test\main.scss:6 DEBUG: null
```

### &#10022; Add Map Items:

Add or append a new key and value pair to the existing map with built-in function called `map.set()`. This accepts three arguments, first one will be map, middle one will be key and last one will be value.

```scss
@use 'sass:map';

$colors: ('primary': blue, 'success': green, 'danger': red);

@debug map.set($colors, 'secondary', gray);
```

*Respective Compilation Message:* 

```bash
test\main.scss:5 DEBUG: ("primary": blue, "success": green, "danger": red, "secondary": gray)
```

### &#10022; Merging Maps:

Instead of, adding one by one; Sass provides possibility to merge two maps using built-in function called `map.merge()`. It accepts two arguments and both should be map. If either of the key gets matched then last map key value will be taken.

```scss
@use 'sass:map';

$colors: ('primary': blue, 'success': green, 'danger': red);
$another-colors: ('secondary': gray, 'danger': pink);

@debug map.merge($colors, $another-colors);
```

*Respective Compilation Message:*

```bash
test\main.scss:6 DEBUG: ("primary": blue, "success": green, "danger": pink, "secondary": gray)
```

### &#10022; Update Map Value:

Sass provides function to set value to existing key-value pair in a map.

```scss
@use 'sass:map';

$colors: (
  "primary": blue,
  "success": green    
);

$text-1: (
  "colors": (
    "primary": blue,
    "success": green    
  ),
  "size": (
    "small": 12px
  )
);

@debug map.set($colors, "primary", pink);
@debug map.set($text-1, "size", "small", 14px);
```

*Respective Compilation Message:*

```bash
test\main.scss:18 DEBUG: ("primary": pink, "success": green)
test\main.scss:19 DEBUG: ("colors": ("primary": blue, "success": green), "size": ("small": 14px))
```

### &#10022; Maps Deep Merge:

It is similar to `map.merge` function, but it merge multi-level maps into single map.

```scss
@use 'sass:map';

$text-1: (
  "colors": (
    "primary": blue,
    "success": green    
  ),
  "size": (
    "small": 12px
  )
);

$text-2: (
  "colors": (
    "danger": red
  ),
  "size": (
    "medium": 16px,
    "large": 20px
  )
);

@debug map.deep-merge($text-1, $text-2);
```

*Respective Compilation Message:*

```bash
test\main.scss:23 DEBUG: ("colors": ("primary": blue, "success": green, "danger": red), "size": ("small": 12px, "medium": 16px, "large": 20px))
```

### &#10022; Map Remove:

Sass provides function to remove specified key-value pair from map.

```scss
@use 'sass:map';

$text-1: (
  "colors": (
    "primary": blue,
    "success": green    
  ),
  "size": (
    "small": 12px
  )
);

@debug map.remove($text-1, "colors");
@debug map-remove($text-1, "size");
```

*Respective Compilation Message:*

```bash
test\main.scss:13 DEBUG: ("size": ("small": 12px))
test\main.scss:14 DEBUG: ("colors": ("primary": blue, "success": green))
```

### &#10022; Map Deep Remove:

Sass provides function to remove specific key-value pair or multiple keys from a map followed by consecutive arguments after the map value specified.

```scss
@use 'sass:map';

$text-1: (
  "colors": (
    "primary": blue, 
    "success": green, 
    "danger": red
  ), 
  "size": (
    "small": 12px, 
    "medium": 16px, 
    "large": 20px
  )
);

@debug map.deep-remove($text-1, "size", "medium");
```

*Respective Compilation Message:*

```bash
test\main.scss:16 DEBUG: ("colors": ("primary": blue, "success": green, "danger": red), "size": ("small": 12px, "large": 20px))
```

### &#10022; Check Map Key Exist:

Sass provides function to check whether the key exists in the map or not.

```scss
@use 'sass:map';

$text-1: (
  "colors": (
    "primary": blue, 
    "success": green, 
    "danger": red
  ), 
  "size": (
    "small": 12px, 
    "medium": 16px, 
    "large": 20px
  )
);

@debug map.has-key($text-1, "colors");
@debug map-has-key($text-1, "size", "extra-large");
```

*Respective Compilation Message:*

```bash
test\main.scss:16 DEBUG: true
test\main.scss:17 DEBUG: false
```

### &#10022; Get Map Keys:

Sass provides function to get map keys as comma separated list items.

```scss
@use 'sass:map';

$text-1: (
  "colors": (
    "primary": blue, 
    "success": green, 
    "danger": red
  ), 
  "size": (
    "small": 12px, 
    "medium": 16px, 
    "large": 20px
  )
);

@debug map.keys($text-1);
@debug map-keys($text-1);
```

*Respective Compilation Message:*

```bash
test\main.scss:16 DEBUG: "colors", "size"
test\main.scss:17 DEBUG: "colors", "size"
```

### &#10022; Get Map Values:

Sass provides function to get map values as a comma separated list items.

```scss
@use 'sass:map';

$text-1: (
  "colors": (
    "primary": blue,
    "success": green    
  ),
  "size": (
    "small": 12px
  )
);

@debug map.values($text-1);
@debug map-values($text-1);
```

*Respective Compilation Message:*

```bash
test\main.scss:13 DEBUG: ("primary": blue, "success": green), ("small": 12px)
test\main.scss:14 DEBUG: ("primary": blue, "success": green), ("small": 12px)
```

### &#10022; Lists:

Lists are sequences of different values separated by commas or spaces or slashes. Sass does not require any brackets to determine as list, but some list may has a brackets. 

```scss
$colors: red, green, blue;
$paddings: (0.5rem 1rem 0.5rem 0); 
```

But Sass allows the list items to be within the square brackets for `grid-template-columns` to treat as multi line `([line1 line2])`.

Sass lists items may starts from zero or an empty elements to whatever items specified into it. 

A one item list can be written in two of the either method. 

```scss
$list: (<expression>,);

$another-list: [<expression>];
``` 

A zero item list can be written either `()` or `[]`. 

Sass functions and similar things treats individual item are not in the list. So, it is required to create atleast a one item list explicitly. 

And an empty list without any of the brackets will not be consider as a list.

List with slashes can be used for different purposes as below:

```scss
p {
  color: hsl(33 80% 70% / 0.75);
}
```

### &#10022; List Indexes:

List items can be targeted by index starting from 1 to their length. For negative index will refer from last items in descending order such as `-1` refers to last item, `-2` refers to 2nd most last item from the list and so on.

### &#10022; Accessing List Length:

Sass provides function to get total number of items in a list.

```scss
@use 'sass:list';
$list1: [red green blue];
$list2: black, white;

@debug list.length($list1);
@debug length($list2);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: 3
test\main.scss:6 DEBUG: 2
```

### &#10022; Identifying List Separator:

Sass provides function to get type of separator used in a list.

```scss
@use 'sass:list';
$list1: [red green blue];
$list2: black, white;

@debug list.separator($list1);
@debug list-separator($list2);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: space
test\main.scss:6 DEBUG: comma
```

### &#10022; Accessing List Item:

List item can be accessed with the built-in function called `nth()`. It accepts two arguments the first one will be list and last one will be index to access the item.

```scss
@use 'sass:list';

@debug list.nth(red green blue, 1);
@debug nth([line1, line2, line3], -1);
```

*Respective Compilation Message:*

```bash
test\main.scss:3 DEBUG: red
test\main.scss:4 DEBUG: line3
```

### &#10022; Update List Item:

Sass provides function to set value to an existing list item.

```scss
@use 'sass:list';
$list1: [red green blue];
$list2: black, white;

@debug list.set-nth($list1, 2, yellow);
@debug set-nth($list2, 1, dark);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: [red yellow blue]
test\main.scss:6 DEBUG: dark, white
```

### &#10022; Get Slash Separated List:

Sass provides function to get normal list into slash separated list.

```scss
@use 'sass:list';
$list1: [red green blue];
$list2: black, white;

@debug list.slash($list1...);
@debug list.slash(black, white);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: red / green / blue
test\main.scss:6 DEBUG: black / white
```

### &#10022; Iterating List Items:

`@each` function can be used to iterate through all list items.

```scss
$colors: ('red', 'green', 'blue');

@each $color in $colors {
  .button-#{$color} {
    background-color: unquote($color);
  }
}
```

*Respective CSS Output:*

```css
.button-red {
  background-color: red;
}

.button-green {
  background-color: green;
}

.button-blue {
  background-color: blue;
}
```

### &#10022; Append List Item:

New item can be appended to an existing list with the built-in function called `list.append()` or simply used as `append()`. The first argument accepts a list and last argument accepts a item.

```scss
@use "sass:list";

$colors: ('red', 'green', 'blue');
$grid-template: ([line1-col1 line1-col2]);

$colors: list.append($colors, 'yellow');
@debug $colors;

$colors: append($colors, 'purple');
@debug $colors;

$grid-template: list.append($grid-template, line1-col3);
@debug $grid-template;
```

*Respective Compilation Message:*

```bash
test\main.scss:7 DEBUG: "red", "green", "blue", "yellow"
test\main.scss:10 DEBUG: "red", "green", "blue", "yellow", "purple"
test\main.scss:13 DEBUG: [line1-col1 line1-col2 line1-col3]
```

### &#10022; Join List Items:

Sass provides function to join two different list together. That accepts two list arguments with separator and bracketed arguments.

$separator argument accepts one of these value comma, space or slash. That will return joined list with one of the separator specified. If auto value specified then it will take separator from first if it has otherwise it will take from last list separator. No other separator value will be accepted.

$bracketed argument accepts boolean true and false. If it is boolean true then it will adds brackets otherwise it will return without brackets. By default, it takes auto, the returned list will be bracketed if first list has.

```scss
@use 'sass:list';
$list1: [red green blue];
$list2: black, white;

@debug list.join($list1, $list2, $separator: auto, $bracketed: auto);
@debug list.join($list1, $list2, $separator: comma, $bracketed: false);
@debug join($list1, $list2, $separator: space, $bracketed: true);
```

*Respective Compilation Message:*

```bash
test\main.scss:5 DEBUG: [red green blue black white]
test\main.scss:6 DEBUG: red, green, blue, black, white
test\main.scss:7 DEBUG: [red green blue black white]
```

### &#10022; Zip Multiple Lists:

It is similar to join function, but it combines multiple list together into combined list of sub-lists.

```scss
@use 'sass:list';
$list1: [red green blue];
$list2: black, white;
$list3: red green blue, black white;

@debug list.zip($list3...);
@debug zip($list1, $list2);
```

*Respective Compilation Message:*

```bash
test\main.scss:6 DEBUG: red black, green white
test\main.scss:7 DEBUG: red black, green white
```



### &#10022; Find List Item Index:

Specific list item position or index can be find using the built-in function called `list.index()`. This function will accept first argument as list and last argument as item value.

```scss
@use "sass:list";

$colors: ('red', 'green', 'blue');
$grid-template: ([line1-col1 line1-col2]);

@debug list.index($colors, 'blue');
```

*Respective Compilation Message:* 

```bash
test\main.scss:6 DEBUG: 3
```

If the item value is not found in the list then it will return `null`. It is treated as `false` or equivalent to boolean `false` to use with control flow directives.

```scss
@use "sass:list";

$colors: ('red', 'green', 'blue');
$color: 'purple';

@if not list.index($colors, $color) {
  @error "#{$color} is not allowed. Choose from one of the #{$colors}.";
}
```

*Respective Compilation Message:*

```bash
Error: "purple is not allowed. Choose from one of the red, green, blue."
  ╷
7 │     @error "#{$color} is not allowed. Choose from one of the #{$colors}.";
  │     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ╵
  test\main.scss 7:2  root stylesheet
```

### &#10022; Argument List:

When number of arguments are passed to a `@mixin` or a `@function` will be treated as a list of items.

```scss
$colors: ('red', 'green', 'blue');
$color-schemes: ('primary': blue, 'success': green, 'danger': red);

@mixin buttons($args...) {
  @debug $args;
}

@include buttons($colors);
@include buttons($color-schemes);
```

*Respective Compilation Message:*

```css
test\main.scss:5 DEBUG: (("red", "green", "blue"),)
test\main.scss:5 DEBUG: (("primary": blue, "success": green, "danger": red),)
```

### &#10022; List Bracketed Function:

Sass provides function to check whether given list is bracketed or unbracketed.

```scss
@use 'sass:list';
$list: red green blue;

@debug list.is-bracketed($list);
@debug is-bracketed($list);
```

*Respective Compilation Message:*

```bash
test\main.scss:4 DEBUG: false
test\main.scss:5 DEBUG: false
```

---
[&#8682; To Top](#-maps-and-list)

[&#10094; Previous Topic](./control-directives.md) &emsp; [Next Topic &#10095;](./modules.md)

[&#8962; Goto Home Page](../README.md)