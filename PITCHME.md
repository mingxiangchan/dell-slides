### CSS Basics

---

### Webpage Building Blocks

- HTML: content
- CSS: styling
- JS: interactivity

---

### Writing CSS

- Target HTML elements using `css selectors`
- Define CSS styling rules for targted elements

---

### Basic CSS: Text

- Changing text 
    - font family
    - alignment
    - colors
    - word-wrap

+++

- Change element
    - background color
    - borders
    - width/height/margins/padding

+++

### Links:

- [Background](https://devdocs.io/css/background)
- [Border](https://devdocs.io/css/border)
- [Font Styling](https://devdocs.io/css/font)
- [Font Color](https://devdocs.io/css/color)
- [Text Styling](https://devdocs.io/css-text/)

---

### CSS Selectors

- Using HTML element tag
- Using `class`
- Using `id`

+++

### Based on HTML element

```html
<body>
    Haha
    <p>Hello</p>
</body>
```


```css
body {
    color: red;
}

p {
    color: green;
}
```

+++

### Based on HTML class

```html
<div class="haha">
    Haha
</div>
<div class="hoho">
    Hoho
</div>
```


```css
.haha {
    color: red;
}

.hoho {
    color: green;
}
```

+++

### Based on HTML id

```html
<div id="haha">
    Haha
</div>
<div id="hoho">
    Hoho
</div>
```


```css
#haha {
    color: red;
}

#hoho {
    color: green;
}
```

+++

### Combined

```html
<div id="haha">
    Haha
</div>
<div class="hoho">
    Hoho
</div>
<p class="hoho">
    Hoho
</p>
```

```css
div#haha {
    color: red;
}

div.hoho {
    color: green;
}
```

---

### Exercise

![resume-site](./resume.jpg)

---

### CSS Layout

1. Everything is boxes
2. Start from the top-left
3. Child top-left -> Parent's top-left

---

### Box Model

- content
- padding
- border
- margin

+++

![box-model](./boxmodel.gif)

+++

### Exercise

- wireframe the resume site using [draw.io](https://www.draw.io/)
- draw the box model for each element in the wireframe
- consider which parts will be content/padding/margin

+++

### Exercise

![resume-site](./resume.jpg)

---


