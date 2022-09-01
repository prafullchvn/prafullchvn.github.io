---
title: 'Isolation Property'
date: 2022-09-01T17:48:22+05:30
draft: false
tags:
  - CSS
  - z-index
---

### z-index

Z index is used to push the element to behind some other element on HTML page.

Syntax :

```css
z-index: <number>;
```

But z-index by default pushed it to the back of element with respect to whole document.

But sometime this is not case. We want to push the element to back in particular group of elements and not with respect to document elements.

So in that case you can use isolation property on parent element to isolate it from other element in document and then you can put z-index on it.
Isolation property takes value `isolate`, `revert`, `revert-layer`.
To make make z-index work relative to particular group of elements then use `isolate` value with `isolation`

In short term,

> isolation property creates new stacking context.

```css
z-index: -1;
isolation: isolate;
```
