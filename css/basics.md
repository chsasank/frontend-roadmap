---
parent: CSS
nav_order: 1
---

# CSS Basics

CSS (Cascading Style Sheets) is the code that styles web content. We'll answer questions like: How do I make text red? How do I make content display at a certain location in the (webpage) layout? How do I decorate my webpage with background images and colors? [Reference](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)

CSS is not a programming languages, just like html. Here's how it looks like:

```css
p {
  color: red;
}
```

Save this in a file called `styles.css`. Now we can include it in our html file by adding the following line in `head`.

```html
<link href="style.css" rel="stylesheet" />
```

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/css-declaration-small.png)

| Part name      | Explanation                                    | In example     |
| -------------- | ---------------------------------------------- | -------------- |
| Selector       | What HTML elements to apply this style/rule on | `<p>` elements |
| Declaration    | How you want to style                          | `color: red;`  |
| Property       | what's the property of style                   | `color`        |
| Property Value | Value of that property                         | `red`          |

You can have multiple properties in a rule set.

```css
p {
  color: red;
  width: 500px;
  border: 1px solid black;
}
```

You can also apply the style to multiple elements

```css
p,
li,
h1 {
  color: red;
}
```

You can have many different type of html selectors to make your rule as specific as you want.

| Selector name         | What it does                         | Example     |
| --------------------- | ------------------------------------ | ----------- |
| Element selector      | All HTML elements of specified type  | `p`         |
| ID selector           | HTML element with specific id        | `#my-id`    |
| Class selector        | All HTML elements of specified class | `.my-class` |
| Attribute selector    | Elements with specified attribute    | `img[src]`  |
| Pseudo-class selector | Element only when in specified state | `a:hover`   |

CSS is all about boxes. HTML elements can be thought of boxes sitting on top of other boxes.

![](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/box-model.png)

```css
h1 {
  margin: 0;
  padding: 20px 0;
  color: #00539f;
}
```

Google fonts are ultra useful for styling. To use them find the font use want and add the css to `head`

```html
<link
  href="https://fonts.googleapis.com/css?family=Open+Sans"
  rel="stylesheet"
/>
```

## Example

Add this to index.html

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Sasank's page</title>
    <link
      href="https://fonts.googleapis.com/css?family=Open+Sans"
      rel="stylesheet"
    />
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <h1>Welcome to Sasank's page</h1>
    <p>Learn about me in this page. You can find me on</p>
    <ol>
      <li id="twitter">Twitter</li>
      <li class="other">Facebook</li>
      <li class="other">Linkedin</li>
    </ol>
    <p>Thanks for visiting my page</p>
  </body>
</html>
```

And this to style.css

```css
html {
  background-color: #00539f;
  font: "Open Sans", sans-serif;
  font-size: 20px;
}

body {
  width: 600px;
  margin: 20px auto;
  background-color: #ff9500;
  padding: 0 20px 20px 20px;
  border: 5px solid black;
}

h1 {
  margin: 0;
  padding: 20px 0;
  color: #00539f;
}

#twitter {
  color: red;
}

.other {
  color: blue;
}
```

Open index.html in your browser and see colorful page.

![image](https://user-images.githubusercontent.com/9305875/121774005-5289d200-cb9d-11eb-9f93-0e0e238fff32.png)
