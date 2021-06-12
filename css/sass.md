---
parent: CSS
nav_order: 2
---

# Sass

{: .no_toc }

Sass (or Syntactically Awesome Style Sheets) is CSS extension language that adds features such as variables, nesting, mixins and more. Sass is very similar to css. [Reference](https://learnxinyminutes.com/docs/sass/).

## Install and usage

`sass` compiles scss files to standard css.

```
$ npm install -g sass
$ sass index.scss build/index.css
```

Alternatively, use npx to run sass without installing anything

```
$ npx sass index.scss build/index.css
```

## Variables

You can store a CSS value (such as a color) in a variable. You can reuse the variables in multiple places so that variables are in one place.

```scss
$primary-color: #a3a4ff;
$secondary-color: #51527f;
$body-font: "Roboto", sans-serif;

body {
  background-color: $primary-color;
  color: $secondary-color;
  font-family: $body-font;
}
```

## Control directives

if/else

```scss
$debug: true !default;

.info {
  @if $debug {
    display: inline-block;
  } @else {
    display: none;
  }
}
```

for loop

```scss
@for $c from 1 to 4 {
  div:nth-of-type(#{$c}) {
    left: ($c - 1) * 900 / 3;
  }
}
```

while loop

```scss
$columns: 4;
$column-width: 80px;

@while $columns > 0 {
  .col-#{$columns} {
    width: $column-width;
    left: $column-width * ($columns - 1);
  }

  $columns: $columns - 1;
}
```

@each functions like for except for list. Note lists just use spaces as delimiters.

```scss
$social-links: facebook twitter linkedin reddit;

.social-links {
  @each $sm in $social-links {
    .icon-#{$sm} {
      background-image: url("images/#{$sm}.png");
    }
  }
}
```

## Mixins, functions etc

If you find you are writing the same code for more than one element, you might want to store that code in a mixin.

```scss
@mixin center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
}

/* You can use the mixin with '@include' and the mixin name. */

div {
  @include center;
  background-color: red;
}
```

You can also have parametric mixins

```scss
@mixin size($width, $height) {
  width: $width;
  height: $height;
}

.rectangle {
  @include size(100px, 60px);
}
```

You can create functions to do cool stuff. Note that they're kinda like mixins.

```scss
@function calculate-percentage($target-size, $parent-size) {
  @return $target-size / $parent-size * 100%;
}

$main-content: calculate-percentage(600px, 960px);

.main-content {
  width: $main-content;
}
```

Extend can be used to inherit other css rules.

```
.display {
    @include size(5em, 5em);
    border: 5px solid $secondary-color;
}

.display-success {
    @extend .display;
    border-color: #22df56;
}
```

Nesting allows you to nest selectors within selectors

```scss
ul {
  list-style-type: none;
  margin-top: 2em;

  li {
    background-color: #ff0000;
  }
}
```

You can modularize css with imports. Create `_reset.scss` and import it in your `styles.scss`

```scss
// _reset.css
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}
```

```scss
@import "reset";

body {
  font-size: 16px;
  font-family: Helvetica, Arial, Sans-serif;
}
```
