---
layout: post
title:      "Selecting a CSS Selector"
date:       2019-02-04 18:50:20 +0000
permalink:  selecting_a_css_selector
---


One area I'm trying to improve my abilities on is CSS. I've noticed that it's something that seems to come with practice and knowing what your options are. I thought I'd put together a post with some CSS selector options (with explanations) to help you decide what is the best one for you to use!



CSS Syntax: 

![https://i.imgur.com/7tYrci3.png](https://i.imgur.com/7tYrci3.png)


# Selectors: 
* **Type**:  `p {…}`
* **Id**:  `#box {…}`
* **Class**:  `.thick {…}`
* **Compound**:   `h1, h2, #box {…}`
* **Descendent**: `#nav li {…}`
* **Child**:  `#list > li {…}`
* **Sibling**:  `h3 + p {…}`
* **Preceded**:  `.styleafter ~ h2 {…}`
* **Universal**: `* {…}`
* **Attribute**: `img[alt="Cat"] {…}`
* **Psuedo**: `li:first-child {…}
a:link {…}`


## Type Selectors:

```
p { 
    color:black;
}
```

Selects all elements with the matching selector name.

`<p>Lorem Ipsum</p>`


## ID Selectors:

```
#box { 
    background:blue;
}
```

Selects all elements with an id attribute value matching the selector name.

`<div id="box">I’m a box.</div>`


## Class Selectors: 

```
.thick { 
    font-weight:bold;
}
```

Selects all elements with a class attribute value matching the selector name.

`<span class="thick">I’m thick.</span>`


## Compound Selectors:

```
h1, h2, #box {
    font-family:Arial,Helvetica, Sans-serif;
}
```

Selects all matched elements in the compound set.

```
<h1>Header</h1>
<h2>Subhead</h2>
<div id="box">I’m a box</div>
```


## Descendent Selector: 

```
#nav li { 
    color:black;
}
```

Selects elements that are descendants of the matching selector name.

```
<ul id="nav">
    <li>child</li>
</ul>
```


## Child Selector: 

```
#list > li { 
    color:black;
}
```

Select only the elements that are direct children of the matching selector name (not grandchildren)

```
<ul id="list”>
   <li>child
     <ul><li>grandchild</li></ul>
   </li>
</ul>
```

## Sibling Selector: 

```
h3 + p { 
    color:black;
}
```

Selects only sibling elements that appear directly after the matching selector name.

```
<h3>An h3 Element</h3>
<p>I'm a p directly after an h3 element.</p>
<p>Not selected</p>
```

## Preceded Selector: 

```
.styleafter ~ h2 { 
    color:black;
}
```

Styles all matched elements preceding after the selector name.

```
<p class="styleafter">Class of styleafter.</p>
<h2>I'm an h2 positioned after</h2>
```

## Universal Selector: 

`* {…}` 

This will style anything that has not been previously styled by anything else.

```
* { 
    color:black;
}
```

## Attribute Selector:

```
img[alt="Cat"] { 
    border: 1px solid black;
}
```

Selects elements who have an attribute with matching value condition.


`<img src="myimage.jpg" alt="Cat">`


![https://i.imgur.com/uySQtOZ.png?1](https://i.imgur.com/uySQtOZ.png?1)


![https://i.imgur.com/ngXcTo6.png?1](https://i.imgur.com/ngXcTo6.png?1)


## Pseudo Selector:

```
a:link { 
    text-decoration:none;
}
```

Selects elements based on a particular event state or relationship among other elements.

`<a href="#">link</a>`

![https://i.imgur.com/TQaWiDH.png?1](https://i.imgur.com/TQaWiDH.png?1)

```
p:first-child { color: blue; } 
p:last-child { color: green;}
```

```
<p>Lorem</p>
<p>Ipsum</p>
<p>Dolores</p>
```

## Authority/Inheritance Rules:
If you use conflicting styles on the same element, ID over rules Class which over rules Type which over rules * (universal). Generally the more specific a selector the more authority it has. If a more specific selector is not defined for an element it will inherit styles from a previously defined general selector statement.

If multiple Classes are applied to the same element, the Class listed furthest to the right over rules its neighbors to the left.

Uses “last man” rule. When conflicts with equal authority arise, CSS will listen to the last style it was told to apply. 


## CSS Color Values: 
* **Names**- There are 147 color names, 16 of which are standard: aqua, black, blue, fuchsia, (gray, grey), green, lime, maroon, navy, olive, purple, red, silver, teal, white, and yellow.
* **Hexadecimal**- There are exactly 16,777,216 (see 16 million colors). These colors when used in different combinations can produce any color that is needed. 
     * For example, in the color red, the color code is #FF0000, which is '255' red, '0' green, and '0' blue. Hex system values use combinations of the characters 0-9 as well as A-F.
* **Rgb and Rgba**- RGB (Red Green Blue) and RGBA (Red Green Blue Alpha) offer millions of colors by mixing varying amounts of red green and blue light; using a scale of (0-255).
     * rgb(100,86,92);
     * A (Alpha) allows an additional accepted value from 0-1 (0%-100% opacity)
     * rgba(100,86,92,0.5);



## Font Declarations: 
* ** font-family**: Arial, Helvetica, sans-serif;
* **font-style**: normal | italic;
* **font-siz**e: 100% | 1em | 12pt | 12px;
* **font-weight**: normal | bold; 
*** color**: white | #fff | rgba(255,255,255,1);
* **font**: bold 1em/2em Arial, sans-serif; 


## Text Declarations: 

* **text-align**: left | center | right;
* ** text-decoration**: none | underline | overline | line-through;
* **text-indent**: 1% | 1em | 1pt | 1px;
* **text-shadow**: 3px 3px 10px #000;
* **text-transform**: none | capitalize | lowercase | uppercase;
* **letter-spacing**: normal | 1em | 12px | 12pt;
* **line-height**: normal | 1em | 12px | 12pt;
* **word-spacing**: normal | 1em | 12px | 12pt;
* **word-wrap**: normal | break-word;
* **white-space**: normal | no-wrap;


## Using Web Fonts: 

![https://i.imgur.com/Nwzirp2.jpg](https://i.imgur.com/Nwzirp2.jpg)

```
@font-face {
    font-family: ‘Skolar’;
    src: url(../fonts/Skolar.webfont);
}
p { font-family: ‘Skolar’, Georgia, serif; } 
```

**Comments: **
```
/* In CSS 
    we can create
    Multi line comments
    like this */
```



![https://i.imgur.com/GamrJjR.gif](https://i.imgur.com/GamrJjR.gif)





