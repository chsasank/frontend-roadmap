---
parent: React
nav_order: 1
---

# React Basics

It is _the_ most awesome UI framework out there. In my words, it applies OOP concepts to frontend. If you ever coded up in jQuery or DOM manipulation directly, you'll understand why react is required. [Reference](https://reactjs.org/tutorial/tutorial.html#overview).

`create-react-app` Creates a react app with pretty much all you need.

```
$ npx create-react-app my-app
$ cd my-app
$ npm start
```

## Component

`render()` returns the component we want to display. [JSX syntax](https://reactjs.org/docs/introducing-jsx.html) is used to describe the component. JS code can be used in it using `{}` like below

```js
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}
```

## Props

`props` are properties that are sent to the component. You can use this component inside yet another component. Note how data like name are passed through props.

```js
function ShoppingLists(props) {
  return <div>
    <ShoppingList name="facebook">
    <ShoppingList name="google">
  </div>;
}
```

You can interaction with callbacks like onClick as follows:

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => alert("click")}>
        {this.props.value}
      </button>
    );
  }
}
```

## State

You might want to store state of the component and change it on interaction. Here's how you do it

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => this.setState({ value: "X" })}>
        {this.state.value}
      </button>
    );
  }
}
```

Note that you have to `setState` method because react will update and render the child components.

## Moving up the state

If you want the state to be manipulated by a parent object, you should use props and not state! So this is how you 'move up' `Square`'s state to `Board`'s state using props.

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => this.props.onClick()}>
        {this.props.value}
      </button>
    );
  }
}

class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = "X";
    this.setState({ squares: squares });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = "Next player: X";

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

Note `.slice()` in the `handleClick` function. It creates a copy of our array. We need this is because state should be immutable. If state were mutable, it's very hard to detect and re-render children objects. So, `setState` has to be used instead of mutating the state object.

## Function Components

Function components are easier and simpler value of writing many components. Here's how `Square` function component looks like:

```js
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```
