
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


  Let's go through the **Intermediate React Concepts** that you've mentioned, breaking each topic down with examples to help solidify your understanding.

---

### 1. **useEffect Hook**

The `useEffect` hook is used to handle side effects in functional components, such as fetching data, subscribing to services, or manipulating the DOM.

#### **Side Effects in React (e.g., data fetching, DOM manipulations)**

Side effects include tasks like:
- Fetching data from APIs
- Subscribing to external services
- Directly manipulating the DOM

**Example: Data Fetching:**

```jsx
import React, { useState, useEffect } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.error('Error fetching data:', error));
  }, []); // Empty array means this runs only once, similar to componentDidMount

  return (
    <div>
      <h1>Fetched Data:</h1>
      {data ? (
        <ul>
          {data.map(post => (
            <li key={post.id}>{post.title}</li>
          ))}
        </ul>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
};

export default DataFetcher;
```

- **Explanation**: The `useEffect` hook fetches data from an API when the component mounts, thanks to the empty dependency array (`[]`). This mimics `componentDidMount` in class components.

---

#### **Dependencies Array and Optimizing Effect Re-renders**

You can optimize when a side effect runs by specifying dependencies in the second argument of `useEffect`.

**Example:**

```jsx
import React, { useState, useEffect } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('The count has changed to:', count);
  }, [count]); // Effect runs only when `count` changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;
```

- **Explanation**: The effect only runs when `count` changes. By listing `count` in the dependency array, we optimize the effect to only run when necessary.

---

#### **Cleanup Functions in useEffect**

Sometimes you need to clean up resources like network requests, subscriptions, or timers when a component unmounts or the effect reruns.

**Example: Cleanup Timer:**

```jsx
import React, { useState, useEffect } from 'react';

const Timer = () => {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    // Cleanup function
    return () => clearInterval(timer); // Clears the timer when component unmounts
  }, []); // Empty array means it runs only once (like componentDidMount)

  return <p>{seconds} seconds have passed.</p>;
};

export default Timer;
```

- **Explanation**: The cleanup function (`return () => clearInterval(timer)`) ensures that the interval is cleared when the component is unmounted, preventing memory leaks.

---

### 2. **useContext Hook**

`useContext` allows you to share values across the component tree without passing props manually at every level (avoiding "prop drilling").

#### **Sharing Data Across Components Without Prop Drilling**

You can create a context to share data globally across components.

**Example: Using Context API for Global State**

```jsx
import React, { useState, createContext, useContext } from 'react';

// Create a Context
const ThemeContext = createContext();

const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => setTheme(prev => (prev === 'light' ? 'dark' : 'light'));

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

const ThemeButton = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <button onClick={toggleTheme}>
      Current Theme: {theme}
    </button>
  );
};

const App = () => (
  <ThemeProvider>
    <ThemeButton />
  </ThemeProvider>
);

export default App;
```

- **Explanation**: The `ThemeContext` is used to provide and consume the `theme` state globally without prop drilling. Any child component can access the theme and change it using `useContext`.

---

### 3. **useReducer Hook**

The `useReducer` hook is typically used for managing complex state logic, especially when the next state depends on the previous state.

#### **Managing Complex State Logic with useReducer**

`useReducer` is an alternative to `useState` when you have complex state transitions (e.g., multiple state variables or actions).

**Example: Counter with `useReducer`**

```jsx
import React, { useReducer } from 'react';

// Reducer function
const counterReducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const Counter = () => {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>Decrement</button>
    </div>
  );
};

export default Counter;
```

- **Explanation**: `useReducer` is used for managing state with actions. In this example, `dispatch` sends actions (`'INCREMENT'` or `'DECREMENT'`) to the reducer to update the state.

#### **Understanding Actions, Dispatch, and Reducers**

- **Actions**: Objects with a `type` property that describe the operation.
- **Dispatch**: A function that sends actions to the reducer.
- **Reducer**: A pure function that takes the current state and an action, then returns a new state.

---

### 4. **useRef Hook**

The `useRef` hook allows you to persist values across renders without causing re-renders. It's also used to directly reference DOM elements.

#### **Using Refs to Access and Manipulate DOM Elements Directly**

**Example: Focusing an Input Element**

```jsx
import React, { useRef } from 'react';

const FocusInput = () => {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus(); // Focus the input element
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Click button to focus" />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
};

export default FocusInput;
```

- **Explanation**: The `useRef` hook is used to create a reference (`inputRef`) to the `<input>` element, allowing us to directly manipulate it (e.g., focusing it when the button is clicked).

#### **Keeping Mutable Values Across Renders Without Triggering Re-renders**

`useRef` can store mutable values that don't trigger re-renders, such as a counter or previous state.

**Example: Keeping Track of Previous State**

```jsx
import React, { useState, useEffect, useRef } from 'react';

const PreviousCount = () => {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef(count); // Store previous count value

  // Update ref after every render
  useEffect(() => {
    prevCountRef.current = count;
  }, [count]);

  return (
    <div>
      <p>Current count: {count}</p>
      <p>Previous count: {prevCountRef.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default PreviousCount;
```

- **Explanation**: `useRef` stores the previous count value. It doesn't cause a re-render when updated, so it can store mutable values between renders without triggering unnecessary updates.

---

### 5. **Component Lifecycle in Class Components**

In class components, you have lifecycle methods that allow you to run code at different stages of the component's life, such as when it mounts, updates, or unmounts.

#### **Understanding Lifecycle Methods**

- **`componentDidMount`**: Called after the component is mounted. It's commonly used for data fetching or setting up subscriptions.
- **`componentDidUpdate`**: Called after every update (i.e., when the component’s state or props change).
- **`componentWillUnmount`**: Called before the component is removed from the DOM. Used for cleanup tasks.

**Example: Timer with Lifecycle Methods**

```jsx
import React, { Component } from 'react';

class Timer extends Component {
  state = { seconds: 0 };

  componentDidMount() {
    this.timerID = setInterval(() => {
      this.setState(prevState => ({ seconds: prevState.seconds + 1 }));
    }, 1000
