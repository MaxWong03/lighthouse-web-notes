# React
* React is `declarative`
* React is `component-based`
  * Each `component` can `receive data` and `maintain state`
  * When a `component` `recevies` new `data` or `changes` its `state` then it will `return` `element` that will be `rendered` to the `DOM`

## Props & State
* Two concepts in React that assist you in managing data
* `Props` are the `data passed` from a `parent` component to a `child` component
  * Similar to passing arguments to a function, but a **component can't change the props passed to it**
* `State` is `private data` `managed internally` by the `component`. 

## Declarative Compoenents
* **Transfer the responsibility of manipulating the DOM to React**

## Function Components
* `Components` are like JS `functions`
* `Accept` arbitrary `inputs` (props)
* `Return` react elements describing `what should appear on the screen`

## Class Components
* You can declare React components as ES6 Classes
* But you must `extend React.Component` and `overwrite the render() method`
* The render() method can return React elements

## React.createElement
* Define the type of element
* Define the props
* Define the Childern
* ` React.createElement(type, [props], [...children])`
* Always start component names with a capital letter

## JSX
* Take any JSX expression and render it to the DOM using `ReactDOM.render` (Normally done once)

## Managing State
* `State` allows us to `retain information` across `multiple renders`
* `useState` receives an `initial state` as an argument and `returns an array`
  * The `first element` of the array is the `currenty value for the state`
  * The `second element` is a function that can `update the state and cause a render`

## Controlled Components 
* A controlled components keeps track of what the current value of that tag is

## Conditional Rendering
* A React component retursn a React element
* We can use a condition to decide which React Element to return

## Short Circuiting
In JavaScript:
  * true && expression always evaluates to expression
  * false && expression always evaluates to false

* If our requirement is to render one of two elements based on state, it would be better to use a ternary operator. A common example for this is showing either a login button or a logout button depending on isLoggedIn state.

``` js
{ isLoggedIn ? <Logout /> : <Login /> }
```

## BEM
* `Block`: Encapsulates a standalone entity that is meaningful on its own
* `Element`: An element that is tied to its block
* `Modifier`: An modification to a block or an element

## Storybook
* The building blocks we use to build complex interfaces are regular JavaScript functions that have a specific interface. These functions accept a single argument that we call props and return React elements.

* Each component will accept different props and allow us to trigger events. Building our components in an environment like this allows us to verify that the component looks and behaves the way that we expect without considering external forces.