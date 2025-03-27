
# React Basics

## 1. **JSX (JavaScript XML)**

### Introduction to JSX:
JSX is a syntax extension for JavaScript, often used with React to describe what the UI should look like. It's a mix of HTML and JavaScript that allows us to write HTML-like code in our JavaScript files.

- **Example:**
  ```jsx
  const element = <h1>Hello, World!</h1>;
  ```

JSX looks like HTML but is actually syntactic sugar for `React.createElement()` calls.

---

### Embedding expressions, attributes, and children inside JSX:

- **Expressions inside JSX:**
  You can embed JavaScript expressions inside JSX by wrapping them in curly braces `{}`. For example:

  ```jsx
  const name = 'John';
  const greeting = <h1>Hello, {name}!</h1>;
  ```

- **Attributes:**
  Just like HTML attributes, JSX allows you to set properties for elements. But, JSX uses camelCase for attribute names instead of lowercase, like `className` instead of `class`.

  ```jsx
  const button = <button className="my-button">Click Me</button>;
  ```

- **Children:**
  In JSX, elements can contain children (nested elements). For example:

  ```jsx
  const list = (
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
  );
  ```

---

## 2. **Components**

### Functional Components:
Functional components are simpler and are defined using JavaScript functions. These are the most common type of component in modern React.

- **Example of Functional Component:**

  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}!</h1>;
  }

  // Usage
  <Welcome name="Alice" />
  ```

Functional components only accept `props` and return JSX.

---

### Class Components:
Class components are the older style of defining components. They require extending the `React.Component` class.

- **Example of Class Component:**

  ```jsx
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}!</h1>;
    }
  }

  // Usage
  <Welcome name="Alice" />
  ```

Class components can also have lifecycle methods (though these are less common in modern React, thanks to hooks).

---

## 3. **Props (Properties)**

### Passing data from parent to child components:
Props allow you to pass data from a parent component to a child component. The child component receives them as function arguments.

- **Example:**

  ```jsx
  function Parent() {
    return <Child name="Alice" />;
  }

  function Child(props) {
    return <h1>Hello, {props.name}!</h1>;
  }
  ```

---

### Default props and prop types for validation:

- **Default Props:**
  If a prop is not passed, we can set a default value for it.

  ```jsx
  function Greeting({ name }) {
    return <h1>Hello, {name}!</h1>;
  }

  Greeting.defaultProps = {
    name: 'Stranger'
  };
  ```

- **Prop Types:**
  To validate the type of props, React provides `prop-types`. This helps catch potential errors early in development.

  ```jsx
  import PropTypes from 'prop-types';

  function Greeting({ name }) {
    return <h1>Hello, {name}!</h1>;
  }

  Greeting.propTypes = {
    name: PropTypes.string.isRequired
  };
  ```

---

## 4. **State Management in Functional Components**

### Introduction to `useState` hook:
The `useState` hook allows functional components to manage their state. It returns a pair: the current state value and a function to update it.

- **Example:**

  ```jsx
  import React, { useState } from 'react';

  function Counter() {
    const [count, setCount] = useState(0); // state variable 'count' and setter function 'setCount'

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>Click me</button>
      </div>
    );
  }
  ```

---

### Setting and updating state:
The state in a functional component is updated using the setter function returned by `useState`.

- **Example:**

  ```jsx
  const [count, setCount] = useState(0);

  // Update state
  setCount(count + 1);
  ```

---

### Re-rendering components on state changes:
React re-renders components when their state or props change. In the example above, each time the button is clicked, the state is updated, causing the component to re-render.

---

## 5. **Event Handling**

### Handling events like `onClick`, `onChange`, `onSubmit`:
In React, events are named using camelCase (e.g., `onClick`, `onSubmit`, `onChange`).

- **Example:**

  ```jsx
  function App() {
    const handleClick = () => {
      alert('Button Clicked!');
    };

    return <button onClick={handleClick}>Click me</button>;
  }
  ```

---

### Event binding and handling the `this` keyword:
In class components, event handlers need to be bound to the class instance.

- **Class Component Example:**

  ```jsx
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      this.state = { count: 0 };
      this.handleClick = this.handleClick.bind(this); // Binding `this` explicitly
    }

    handleClick() {
      this.setState({ count: this.state.count + 1 });
    }

    render() {
      return (
        <button onClick={this.handleClick}>
          You clicked {this.state.count} times
        </button>
      );
    }
  }
  ```

In functional components with hooks, there is no need to bind `this`.

---

## 6. **Conditional Rendering**

### Conditional rendering with ternary operators or `&&`:

- **Using Ternary Operators:**

  ```jsx
  function Greeting({ isLoggedIn }) {
    return isLoggedIn ? <h1>Welcome Back!</h1> : <h1>Please Log In</h1>;
  }
  ```

- **Using `&&`:**

  ```jsx
  function Notification({ message }) {
    return message && <p>{message}</p>; // Renders only if message is not falsy
  }
  ```

### Using `if-else` logic within JSX:
You can also use standard `if-else` logic inside functions, but not directly inside JSX:

  ```jsx
  function Greeting({ isLoggedIn }) {
    let message;
    if (isLoggedIn) {
      message = <h1>Welcome Back!</h1>;
    } else {
      message = <h1>Please Log In</h1>;
    }
    return message;
  }
  ```

---

## 7. **Lists and Keys**

### Rendering lists dynamically using the `.map()` function:
The `.map()` function is used to iterate over an array and render a list of elements.

- **Example:**

  ```jsx
  const fruits = ['Apple', 'Banana', 'Cherry'];

  function FruitList() {
    return (
      <ul>
        {fruits.map((fruit, index) => (
          <li key={index}>{fruit}</li>
        ))}
      </ul>
    );
  }
  ```

---

### Understanding the importance of keys for performance optimization:
React uses keys to identify which items in the list are changed, added, or removed. This helps React optimize re-rendering of lists and improves performance.

- **Important:**
  Keys should be unique for each element in the list.

  ```jsx
  {fruits.map((fruit) => (
    <li key={fruit}>{fruit}</li>  // Using the item itself as a key
  ))}
  ```
