## React-questions


## Q.1 What is  React?
React is an open-source front-end JavaScript library that is used for building user interfaces, especially for single-page applications. It is used for handling view layer for web and mobile apps. React was created by Jordan Walke, a software engineer working for Facebook. React was first deployed on Facebook's News Feed in 2011 and on Instagram in 2012.

## Q.2 What are the major features of React?
The major features of React are:
- It uses VirtualDOM instead of RealDOM considering that RealDOM manipulations are expensive.
- Supports server-side rendering.
- Follows Unidirectional data flow or data binding.
- Uses reusable/composable UI components to develop the view.

## Q.3 What is JSX?
JSX is a XML-like syntax extension to ECMAScript (the acronym stands for JavaScript XML). Basically it just provides syntactic sugar for the React.createElement() function, giving us expressiveness of JavaScript along with HTML like template syntax.

In the example below text inside `<h1>` tag is returned as JavaScript function to the render function.

```js
class App extends React.Component {
  render() {
    return(
      <div>
        <h1>{'Welcome to React world!'}</h1>
      </div>
    )
  }
}
```
## Q.4 What is the difference between Element and Component?
An Element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components. Elements can contain other Elements in their props. Creating a React element is cheap. Once an element is created, it is never mutated.

The object representation of React Element would be as follows:
```js
const element = React.createElement(
  'div',
  {id: 'login-btn'},
  'Login'
)
The above React.createElement() function returns an object:

{
  type: 'div',
  props: {
    children: 'Login',
    id: 'login-btn'
  }
}
And finally it renders to the DOM using ReactDOM.render():

<div id='login-btn'>Login</div>
```
Whereas a component can be declared in several different ways. It can be a class with a render() method or it can be defined as a function. In either case, it takes props as an input, and returns a JSX tree as the output:
```js
const Button = ({ onLogin }) =>
  <div id={'login-btn'} onClick={onLogin}>Login</div>
Then JSX gets transpiled to a React.createElement() function tree:

const Button = ({ onLogin }) => React.createElement(
  'div',
  { id: 'login-btn', onClick: onLogin },
  'Login'
)
```
## Q.5 How to create components in React?
There are two possible ways to create a component.

- Function Components: This is the simplest way to create a component. Those are pure JavaScript functions that accept props object as the first parameter and return React elements:
```js
function Greeting({ message }) {
  return <h1>{`Hello, ${message}`}</h1>

}
```
- Class Components: You can also use ES6 class to define a component. The above function component can be written as:
```js
class Greeting extends React.Component {
  render() {
    return <h1>{`Hello, ${this.props.message}`}</h1>
  }
}
```
## Q.6 What is state in React?
- State of a component is an object that holds some information that may change over the lifetime of the component. We should always try to make our state as simple as possible and minimize the number of stateful components.
- State is used for internal communication inside a components.

Let's create a user component with message state
```js
class User extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      message: 'Welcome to React world'
    }
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    )
  }
}
```
## Q.7 What are props in React?
React Props are like function arguments in JavaScript and attributes in HTML.To send props into a component, use the same syntax as HTML attributes. They are data passed down from a parent component to a child component.

The primary purpose of props in React is to provide following component functionality:
- Pass custom data to your component.
- Trigger state changes.
- Use via this.props.reactProp inside component's render() method.
- 
```js
const myElement = <Car brand="Ford" />;

The component receives the argument as a props object:

Use the brand attribute in the component:

function Car(props) {
  return <h2>I am a { props.brand }!</h2>;
}
```
## Q.8 What is the difference between state and props?
Both props and state are plain JavaScript objects. While both of them hold information that influences the output of render, they are different in their functionality with respect to component. Props get passed to the component similar to function parameters whereas state is managed within the component similar to variables declared within a function.

## Q.9 What is the purpose of callback function as an argument of setState()?
The callback function is invoked when setState finished and the component gets rendered. Since setState() is asynchronous the callback function is used for any post action.
```js
setState({ name: 'John' }, () => console.log('The name has updated and component re-rendered'))
```
## Q.10 How to bind methods or event handlers in JSX callbacks?
Arrow functions in callbacks: You can use arrow functions directly in the callbacks.
```js
handleClick() {
    console.log('Click happened');
}
render() {
    return <button onClick={() => this.handleClick()}>Click Me</button>;
}
```
## Q.11 What are Pure Components?
React.PureComponent is exactly the same as React.Component except that it handles the shouldComponentUpdate() method for you. When props or state changes, PureComponent will do a shallow comparison on both props and state. Component on the other hand won't compare current props and state to next out of the box. Thus, the component will re-render by default whenever shouldComponentUpdate is called.

## Q.12 How to pass a parameter to an event handler or callback?
You can use an arrow function to wrap around an event handler and pass parameters:
```js
<button onClick={() => this.handleClick(id)} />
```
## Q.13 What is "key" prop and what is the benefit of using it in arrays of elements?
A key is a special string attribute you should include when creating arrays of elements. Key prop helps React identify which items have changed, are added, or are removed.
```js
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
)
```
When you don't have stable IDs for rendered items, you may use the item index as a key as a last resort:
```js
const todoItems = todos.map((todo, index) =>
  <li key={index}>
    {todo.text}
  </li>
)
```
## Q.14 What is Virtual DOM?
The Virtual DOM (VDOM) is an in-memory representation of Real DOM. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called reconciliation.
## Q.15 How Virtual DOM works?
The Virtual DOM works in three simple steps.
- Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.
- Then the difference between the previous DOM representation and the new one is calculated.
- Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

## Q.16 What is the difference between Shadow DOM and Virtual DOM?
The Shadow DOM is a browser technology designed primarily for scoping variables and CSS in web components. The Virtual DOM is a concept implemented by libraries in JavaScript on top of browser APIs.

## Q.17 What are the different phases of component lifecycle?
The component lifecycle has three distinct lifecycle phases:

**Mounting**: The component is ready to mount in the browser DOM. This phase covers initialization from constructor(), getDerivedStateFromProps(), render(), and `componentDidMount()` lifecycle methods.(Render The component will render without any side effects.)

**Updating**: In this phase, the component gets updated in two ways, sending the new props and updating the state either from setState() or forceUpdate(). This phase covers getDerivedStateFromProps(), shouldComponentUpdate(), render(), getSnapshotBeforeUpdate() and `componentDidUpdate()` lifecycle methods.(Pre-commit Before the component actually applies the changes to the DOM)

**Unmounting**: In this last phase, the component is not needed and gets unmounted from the browser DOM. This phase includes `componentWillUnmount()` lifecycle method.(Commit React works with the DOM and executes the final lifecycles respectively componentDidMount() for mounting, componentDidUpdate() for updating, and componentWillUnmount() for unmounting.)

## Q.17 What are the lifecycle methods of React?
**componentDidMount**: Executed after first rendering and where all AJAX requests, DOM or state updates, and set up event listeners should occur.
**componentDidUpdate**: Mostly it is used to update the DOM in response to prop or state changes. This will not fire if shouldComponentUpdate() returns false.
**componentWillUnmount**: It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.















