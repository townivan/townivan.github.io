---
tags: css
---

# css: Media queries

Classic "mobile first" syntax that basically means "If [device width] is greater than or equal to 800px, then do {…}".

```css
@media (min-width: 500px){
    .btn{ background-color: teal; }
}
```

New range syntax.  [You can use it now](https://caniuse.com/css-container-queries).

```css
@media (width > 600px){
    .btn{ background-color: red; }
}
```

Range syntax:  new "and"

```css
@media (700px < width < 800px){
    .btn{ background-color: pink; }
}
```

Range syntax:  old "and"

```css
@media (width > 900px) and (width < 1000px){
    .btn{ background-color: orange; }
}
```

Some common breakpoints:

* tablets >= 768px
* laptops >= 992px
* desktop >= 1200px
