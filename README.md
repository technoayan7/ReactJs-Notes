# ReactJs-Notes



### Reference - 
***https://www.interviewbit.com/react-interview-questions***

---

### What is React?

React is a JavaScript library for building user interfaces, mainly for single-page applications (SPAs). It uses a component-based structure and a Virtual DOM to optimize rendering, making UI creation more efficient and maintainable.

*The important features of React are:*

1. **It supports server-side rendering.**

2. **It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.**

3. **It follows unidirectional data binding or data flow.**

4. **It uses reusable or composable UI components for developing the view.**

---

### Advantages of Using React

1. **Reusable Components**: Modular components improve development speed and maintainability.
2. **Efficient Rendering**: The Virtual DOM minimizes actual DOM updates, boosting performance.
3. **Flexible**: Can be used for web and mobile apps (with React Native) and works well with other libraries.
4. **Strong Community**: Large ecosystem and support with tools for routing, state management, and testing.
5. **Declarative Syntax**: Easier to read and debug, focusing on *what* the UI should look like.
6. **Developer-Friendly**: JSX offers a syntax that combines HTML and JavaScript, simplifying UI code.

---

### Limitations of React

1. **Steep Learning Curve**: React concepts (like JSX and state) can be challenging for beginners.
2. **JSX Complexity**: JSX syntax requires learning and additional compilation, which can add complexity.
3. **Frequent Updates**: The ecosystem evolves rapidly, requiring developers to keep up with new changes.
4. **Needs Extra Libraries**: Full-scale apps often need additional libraries (like React Router, Redux).
5. **SEO Challenges**: React is primarily client-side, which can hinder SEO without server-side rendering.

### JSX
JSX (JavaScript XML) lets you write HTML-like syntax within JavaScript, making it easier to visualize UI components. It is then transformed into JavaScript objects by React before rendering.

```jsx
const element = <h1>Hello, world!</h1>;
```

### Virtual DOM
The Virtual DOM is a lightweight copy of the actual DOM. React uses this to make updates more efficient. When something changes, React updates the Virtual DOM, compares it to the previous version, and only changes the necessary parts of the actual DOM.

### State
State is like a "memory" for components. It holds data that can change over time (like user input or fetched data) and automatically triggers a re-render when updated.

```jsx
const [count, setCount] = useState(0); // Initializes a count variable with 0 and a function to update it
```

### Props
Props (short for "properties") are read-only data passed from parent to child components. They allow data to flow through the component tree and make components reusable.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Usage
<Welcome name="John" /> // Renders "Hello, John"
```

### Props Drilling
Props drilling happens when data is passed through many layers of components just to reach a deeply nested child component, which can make the code harder to maintain.

```jsx
function Parent() {
  const userName = "John";
  return <Child userName={userName} />;
}

function Child({ userName }) {
  return <GrandChild userName={userName} />;
}

function GrandChild({ userName }) {
  return <p>Hello, {userName}</p>;
}
```

### Context API
The Context API provides a way to pass data through the component tree without having to pass props manually at every level. This helps avoid props drilling.

```jsx
const UserContext = React.createContext(); // Step 1: Create a context

function App() {
  return (
    <UserContext.Provider value={"John"}> // Step 2: Provide context value
      <Component />
    </UserContext.Provider>
  );
}

// Step 3: Consume context in a nested component
function Component() {
  const user = useContext(UserContext);
  return <p>Welcome, {user}</p>; // Outputs "Welcome, John"
}
```

### Class Components vs Functional Components
Class components are built using ES6 classes and have access to lifecycle methods. Functional components are simpler and can use Hooks to manage state and other React features.

```jsx
// Class Component
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

// Functional Component
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### Hooks
Hooks are functions introduced in React that allow you to use state, lifecycle methods, and other features in functional components. Common hooks include `useState`, `useEffect`, and `useContext`.


### useState
`useState` is a hook that lets you add state to a functional component. It returns an array with the current state and a function to update it.

```jsx
const [count, setCount] = useState(0); // Initializes a state variable 'count' with 0 and a function 'setCount'
```

### useEffect
`useEffect` is a hook for managing side effects in components, like data fetching, timers, and subscriptions. It runs after the render and can depend on specific variables.

```jsx
useEffect(() => {
  // This will run when the component mounts or when dependencies change
}, []); // Empty array means it runs only once, on mount
```

### useRef
`useRef` allows you to create a reference to a DOM element or a value that persists between renders without causing a re-render when updated. Commonly used for accessing DOM nodes or storing a mutable value.

```jsx
const inputRef = useRef(); // Creates a reference to an input

function handleClick() {
  inputRef.current.focus(); // Access the DOM node directly
}
```

### useMemo
`useMemo` memoizes a calculated value, meaning it only recalculates when dependencies change. This can help optimize performance by preventing expensive calculations on every render.

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

### useCallback
`useCallback` memoizes a function so it isn’t recreated on every render unless dependencies change. Useful for optimizing child components that depend on callbacks.

```jsx
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

### useReducer
`useReducer` is useful for managing complex state logic, especially when the state depends on previous values. It’s similar to Redux, where a "reducer" function decides how to update the state.

```jsx
const [state, dispatch] = useReducer(reducer, initialState); // Use dispatch to change state based on actions
```

### useContext
`useContext` lets you use values from Context in functional components, avoiding prop drilling.

```jsx
const user = useContext(UserContext);
```

### useLayoutEffect
`useLayoutEffect` works similarly to `useEffect`, but it runs synchronously after all DOM changes. This is useful if you need to make DOM measurements or changes before the browser repaints.

```jsx
useLayoutEffect(() => {
  // Runs immediately after DOM updates
}, []);
```

### Custom Hooks
Custom Hooks let you create reusable logic. For example, a custom hook that fetches data can be shared across multiple components.

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url).then(response => response.json()).then(setData);
  }, [url]);
  return data;
}
```

### Redux
Redux is a state management library that allows you to store the entire application’s state in one place, making it accessible to any component. It uses actions to modify the state.

```js
// Redux action
const increment = () => ({ type: 'INCREMENT' });
```

### Higher Order Components (HOC)
A Higher-Order Component (HOC) is a function that takes a component and returns a new component with additional props or functionality.


```jsx
function withUser(Component) {
  return function EnhancedComponent(props) {
    return <Component {...props} user={"John"} />;
  };
}
```

### When do we need a Higher Order Component?

While developing React applications, we might develop components that are quite similar to each other with minute differences. In most cases, developing similar components might not be an issue but, while developing larger applications we need to keep our code DRY, therefore, we want an abstraction that allows us to define this logic in a single place and share it across components. HOC allows us to create that abstraction.

### Components Lifecycles
There are four different phases in the lifecycle of React component. They are:

1. **Initialization**: During this phase, React component will prepare by setting up the default props and initial state for the upcoming tough journey.

2. **Mounting**: Mounting refers to putting the elements into the browser DOM. Since React uses VirtualDOM, the entire browser DOM which has been currently rendered would not be refreshed. This phase includes the lifecycle methods componentWillMount and componentDidMount.

3. **Updating**: In this phase, a component will be updated when there is a change in the state or props of a component. This phase will have lifecycle methods like componentWillUpdate, shouldComponentUpdate, render, and componentDidUpdate.

4. **Unmounting**: In this last phase of the component lifecycle, the component will be removed from the DOM or will be unmounted from the browser DOM. This phase will have the lifecycle method named componentWillUnmount

### Lifecycle Methods
Lifecycle methods are special functions in class components that control component behavior at each lifecycle stage. For example, `componentDidMount` runs after the component is rendered, and `componentWillUnmount` runs before it’s removed from the DOM.

### Lazy Loading
Lazy loading is a technique that allows components to load only when needed, improving the app’s performance by reducing the initial load time.

```jsx
const LazyComponent = React.lazy(() => import('./LazyComponent'));
```

### React App Performance Optimization Techniques
1. **Use `React.memo`**: Memoizes components to avoid unnecessary re-renders.
2. **Lazy loading with `React.lazy` and `Suspense`**: Reduces initial load time by only loading components when they’re needed.
3. **Avoid inline functions**: Inline functions in JSX can create new instances on every render.
4. **Use `useMemo` and `useCallback`**: Memoize values and functions to prevent recalculating or recreating on every render.
5. **Code Splitting**: Breaks up large code bundles into smaller chunks, so users only download what they need.

--- 
