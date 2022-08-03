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

## Q.18 What are Higher-Order Components?
A higher-order component is a function that takes a component and returns a new component. Basically, it's a pattern that is derived from React's compositional nature.

We call them pure components because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.
It use as
- Code reuse, logic and bootstrap abstraction.
- Render hijacking.
- State abstraction and manipulation.
- Props manipulation.
## Q.19 If you are using ES6 or the Babel transpiler to transform your JSX code then you can accomplish this with computed property names.
```js
handleInputChange(event) {
  this.setState({ [event.target.id]: event.target.value })
}
```
## Q.20 What are the advantages of React?
Below are the list of main advantages of React,
-Increases the application's performance with Virtual DOM.
-JSX makes code easy to read and write.
-It renders both on client and server side (SSR).
-Easy to integrate with frameworks (Angular, Backbone) since it is only a view library.
-Easy to write unit and integration tests with tools such as Jest.
## Q.21 What are the limitations of React?
Apart from the advantages, there are few limitations of React too,
- React is just a view library, not a full framework.
- There is a learning curve for beginners who are new to web development.
- Integrating React into a traditional MVC framework requires some additional configuration.
- The code complexity increases with inline templating and JSX.
- Too many smaller components leading to over engineering or boilerplate.
## Q.22 What is the lifecycle methods order in mounting?
The lifecycle methods are called when an instance of a component is being created and inserted into the DOM.
- constructor()
- static getDerivedStateFromProps()
- render()
- componentDidMount()
## Q.23 What is strict mode in React?
React.StrictMode is a useful component for highlighting potential problems in an application. It does not render any extra DOM elements. It activates additional checks and warnings for its descendants. These checks apply for development mode only.
## Q.24 Why should component names start with capital letter?
If you are rendering your component using JSX, the name of that component has to begin with a capital letter otherwise React will throw an error as an unrecognized tag. This convention is because only HTML elements and SVG tags can begin with a lowercase letter.
## Q.25 How to loop inside JSX?
You can simply use Array.prototype.map with ES6 arrow function syntax.

For example, the items array of objects is mapped into an array of components:
```js
<tbody>
  {items.map(item => <SomeComponent key={item.id} name={item.name} />)}
</tbody>
```
## Q.26 What is the difference between React and ReactDOM?
The react package contains React.createElement(), React.Component, React.Children, and other helpers related to elements and component classes. You can think of these as the isomorphic or universal helpers that you need to build components. The react-dom package contains ReactDOM.render(), and in react-dom/server we have server-side rendering support with ReactDOMServer.renderToString() and ReactDOMServer.renderToStaticMarkup().
## Q.27 How to listen to state changes?
The componentDidUpdate lifecycle method will be called when state changes. You can compare provided state and props values with current state and props to determine if something meaningful changed.
```js
componentDidUpdate(object prevProps, object prevState)
```
## Q.28 Why you can't update props in React?
The React philosophy is that props should be immutable and top-down. This means that a parent can send any prop values to a child, but the child can't modify received props.
## Q.29 What is React Router?
React Router is a powerful routing library built on top of React that helps you add new screens and flows to your application incredibly quickly, all while keeping the URL in sync with what's being displayed on the page.
## Q.30 What is Redux?
Redux is a predictable state container for JavaScript apps based on the Flux design pattern. Redux can be used together with React, or with any other view library. It is tiny (about 2kB) and has no dependencies.
## Q.31 What is flux?
Flux is an application design paradigm used as a replacement for the more traditional MVC pattern. It is not a framework or a library but a new kind of architecture that complements React and the concept of Unidirectional Data Flow. Facebook uses this pattern internally when working with React.
## Q.32 What are the core principles of Redux?
Redux follows three fundamental principles:

- Single source of truth: The state of your whole application is stored in an object tree within a single store. The single state tree makes it easier to keep track of changes over time and debug or inspect the application.
- State is read-only: The only way to change the state is to emit an action, an object describing what happened. This ensures that neither the views nor the network callbacks will ever write directly to the state.
- Changes are made with pure functions: To specify how the state tree is transformed by actions, you write reducers. Reducers are just pure functions that take the previous state and an action as parameters, and return the next state.
## Q.33 What is the mental model of redux-saga?
Saga is like a separate thread in your application, that's solely responsible for side effects. redux-saga is a redux middleware, which means this thread can be started, paused and cancelled from the main application with normal Redux actions, it has access to the full Redux application state and it can dispatch Redux actions as well.
## Q.34 What is Redux Thunk?
Redux Thunk middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met. The inner function receives the store methods dispatch() and getState() as parameters.
## Q.35 What are the differences between redux-saga and redux-thunk?
Both Redux Thunk and Redux Saga take care of dealing with side effects. In most of the scenarios, Thunk uses Promises to deal with them, whereas Saga uses Generators. Thunk is simple to use and Promises are familiar to many developers, Sagas/Generators are more powerful but you will need to learn them. But both middleware can coexist, so you can start with Thunks and introduce Sagas when/if you need them.
## Q.36 What are the differences between Flux and Redux?
Below are the major differences between Flux and Redux
|Flux	|Redux|
|State is mutable |	State is immutable|
|The Store contains both state and change logic	| The Store and change logic are separate|
|There are multiple stores exist |	There is only one store exist|
|All the stores are disconnected and flat |	Single store with hierarchical reducers|
|It has a singleton dispatcher	| There is no concept of dispatcher|
|React components subscribe to the store	| Container components uses connect function|
## Q.37 What are hooks?
Hooks is a special function (introduced as a new feature in React 16.8) that lets you use state and other React features without writing a class.
```js
Let's see an example of useState hook:

import { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
## Q.38 What rules need to be followed for hooks?
You need to follow two rules in order to use hooks,
- Call Hooks only at the top level of your react functions. i.e, You shouldn’t call Hooks inside loops, conditions, or nested functions. This will ensure that Hooks are called in the same order each time a component renders and it preserves the state of Hooks between multiple useState and useEffect calls.
- Call Hooks from React Functions only. i.e, You shouldn’t call Hooks from regular JavaScript functions.
## Q.39What is the difference between Real DOM and Virtual DOM?
Below are the main differences between Real DOM and Virtual DOM,

|Real DOM	| Virtual DOM|
|Updates are slow	| Updates are fast|
|DOM manipulation is very expensive. |	DOM manipulation is very easy|
|You can update HTML directly. |	You Can’t directly update HTML|
|It causes too much of memory wastage |	There is no memory wastage|
|Creates a new DOM if element updates |	It updates the JSX if element update |


































