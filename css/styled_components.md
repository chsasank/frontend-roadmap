---
parent: CSS
nav_order: 4
---

# Styled Components

Oldest method of styling is to have document level css file, something like `styles.css`, that every component uses. Recent css-in-js method of styling allows you to write component level css directly in javascript next to your component. You don't have to worry about name collisions and like. [styled-components](https://styled-components.com/) is one such approach for react.

Here's how you install it:

```bash
# create a new react app if you don't have one already
$ npx create-react-app myapp
$ cd myapp

# install styled-components
$ yarn add styled-components
```

To use styled components, you just put this in your component code

```js
import styled from "styled-components";

const Button = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
`;

function MyComponent(props) {
  return (
    <>
      <p>Hello world</p>
      <Button>I'm a styled button</Button>
    </>
  );
}
```

`Button` is a react component like any other that can be reused. Note how css is actually written in the javascript itself. What if you want to create different types of buttons, say primary button? You can do that using props!

```js
import styled, { css } from "styled-components";

const Button = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;

  ${(props) =>
    props.primary &&
    css`
      background: palevioletred;
      color: white;
    `};
`;

// another component to make things centered
const Container = styled.div`
  text-align: center;
`;

function MyComponent(props) {
  return (
    <Container>
      <p>Hello world</p>
      <Button>I'm a styled button</Button>
      <Button primary={true}>I'm a styled primary button</Button>
    </Container>
  );
}
```
