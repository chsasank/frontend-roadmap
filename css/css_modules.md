---
parent: CSS
nav_order: 3
---

# CSS Modules

A CSS Module is a CSS file in which all class names and animation names are scoped locally by default. It is not an official spec or an implementation in the browser but rather a process in a build step (with the help of Webpack or Browserify) that changes class names and selectors to be scoped. Normally css is global scope and this is problematic. CSS modules fix this by making css local scope by default. [Reference 1](https://github.com/css-modules/css-modules). [Reference 2](https://css-tricks.com/css-modules-part-1-need/)

To use CSS module, create a css file (name ending with `.module.css` seems to be the convention).

```css
/* styles.module.css */
.title {
  background-color: red;
}
```

In your js file, import the css and assign the `styles.title` as class to the element you want.

```js
import styles from "./styles.module.css";

element.innerHTML = `<h1 class="${styles.title}">
     An example heading
   </h1>`;
```

This will generate html (and css) with unique class name, something like this:

```html
<h1 class="_styles__title_309571057">
  An example heading
</h1>
```

So, you don't have to worry about namespace clashes anymore! You can also have composition of classes if you use `composes` keyword. This is similar to sass's `@extend`.

```css
.serifFont {
  font-family: Georgia, serif;
}

.title {
  composes: serifFont;
  background-color: red;
}
```

This will generate html that looks something like this:

```html
<h1 class="_styles__title_309571057 _styles__serifFont_404840">
  An example heading
</h1>
```

You can also have dependencies from other files:

```css
.otherClassName {
  composes: className from "./style.css";
}
```

It is recommended to use cameCase instead of kebab-case. We have to use css modules in conjunction with webpack. However, I recommend using scripts like `create-react-app` or `create-next-app` which support css modules out of the box. If you insist on manual config, follow [this tutorial](https://css-tricks.com/css-modules-part-2-getting-started/).