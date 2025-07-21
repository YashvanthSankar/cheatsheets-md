# Complete React.js Guide

## 1. What is React?

- **React** is a JavaScript library for building user interfaces (UIs).
- It is maintained by Facebook and a community of developers.
- Used to build single-page applications (SPAs) – fast, interactive web apps that don't reload the page.
- React is "declarative": you describe what UI should look like, React updates it efficiently.

---

## 2. Core Concepts

### Components

- Building blocks of React. Each piece of UI is a **component**.
- Components are JavaScript functions or classes that return JSX.

**Example:**
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

### JSX

- **JSX** stands for JavaScript XML.
- Lets you write HTML-like code in your JavaScript files.
- Browsers don’t understand JSX directly – it’s compiled to JavaScript.

**Example:**
```jsx
const element = <h1>Hello, world!</h1>;
```

### Props

- **Props** (short for "properties") are like arguments to components.
- Passed from parent to child components.

**Example:**
```jsx
<Welcome name="Yashvanth" />
```

### State

- **State** is data managed by the component.
- When state changes, the component re-renders.

**Example:**
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---

## 3. Setting Up a React Project

### Using Create React App (Recommended for Beginners)

```sh
npx create-react-app my-app
cd my-app
npm start
```

- Your app runs at `http://localhost:3000`
- Edit `src/App.js` to start coding!

---

## 4. Component Types

### Function Components (Modern)

```jsx
function HelloWorld() {
  return <h1>Hello, World!</h1>;
}
```

### Class Components (Older, Less Common Now)

```jsx
import React, { Component } from 'react';

class HelloWorld extends Component {
  render() {
    return <h1>Hello, World!</h1>;
  }
}
```

---

## 5. React Hooks

- **Hooks** let you use state and other React features in function components.
- Common hooks:
  - `useState` – for state
  - `useEffect` – for side effects (like fetching data)
  - `useContext`, `useReducer`, etc.

**useEffect Example:**

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds(s => s + 1), 1000);
    return () => clearInterval(interval); // Cleanup on unmount
  }, []); // Empty array = run once on mount

  return <p>Seconds: {seconds}</p>;
}
```

---

## 6. Rendering Lists

```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```
- Always use a unique `key` prop when rendering lists.

---

## 7. Handling Events

```jsx
function Button() {
  function handleClick() {
    alert('Clicked!');
  }
  return <button onClick={handleClick}>Click me</button>;
}
```

---

## 8. Conditional Rendering

```jsx
function Greeting({ isLoggedIn }) {
  return isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign in.</h1>;
}
```

---

## 9. Lifting State Up

- Sometimes, you need to share state between components.
- Move ("lift") the state to their closest common parent.

**Example:**
```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <ChildA count={count} />
      <ChildB setCount={setCount} />
    </>
  );
}
```

---

## 10. Composing Components

- Put components inside other components to build complex UIs.

```jsx
function App() {
  return (
    <div>
      <Header />
      <UserList users={users} />
      <Footer />
    </div>
  );
}
```

---

## 11. Fetching Data

- Use `useEffect` for data fetching.

```jsx
import React, { useState, useEffect } from 'react';

function Users() {
  const [users, setUsers] = useState([]);
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(setUsers);
  }, []);
  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}
```

---

## 12. React Router (For Multi-Page Apps)

Install:
```sh
npm install react-router-dom
```

Usage:
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 13. Auditing React Code

When reviewing/auditing React code, check for:

- **Component Structure**: Are components too large? Should they be split?
- **Props & State**: Is state in the right place? Are props being used efficiently?
- **Hooks**: Proper use of hooks (`useState`, `useEffect`, etc.)? Any missing dependency arrays in `useEffect`?
- **Side Effects**: Are effects cleaned up? (e.g., intervals, subscriptions)
- **Performance**: Unnecessary re-renders? Use of `React.memo`, `useCallback` where needed?
- **Accessibility**: Use semantic HTML, proper ARIA labels.
- **Security**: Avoid dangerous HTML (`dangerouslySetInnerHTML`). Sanitize user input.
- **Keys in Lists**: Are they unique and stable?
- **Code Quality**: Consistent formatting, meaningful names, comments where needed.

---

## 14. Best Practices

- **Keep components small and focused.**
- **Reuse components where possible.**
- **Avoid duplicating state.**
- **Use `propTypes` or TypeScript for prop validation.**
- **Don’t mutate state directly.**
- **Use functional updates for state changes that rely on previous state.**
- **Lift state up only when necessary.**
- **Keep side effects in `useEffect`.**
- **Test your components.**

---

## 15. Further Learning Resources

- [The Official React Docs](https://react.dev/)
- [React Tutorial](https://react.dev/learn/tutorial-tic-tac-toe)
- [React Router Docs](https://reactrouter.com/)
- [FreeCodeCamp React Course (YouTube)](https://www.youtube.com/watch?v=bMknfKXIFA8)

---

## 16. Example Project Structure

```
my-app/
  src/
    components/
      Header.js
      Footer.js
      UserList.js
    App.js
    index.js
  public/
  package.json
```

---

## 17. Sample Minimal App

```jsx
// src/App.js
import React, { useState } from 'react';

function App() {
  const [name, setName] = useState('');
  return (
    <div>
      <h1>React Example</h1>
      <input value={name} onChange={e => setName(e.target.value)} placeholder="Your name" />
      <p>Hello, {name || 'stranger'}!</p>
    </div>
  );
}

export default App;
```

---

## 18. Common Mistakes

- Not using keys in lists
- Mutating state directly (`state.value = ...`)
- Forgetting to clean up effects
- Updating state in a loop without batching
- Passing unnecessary props

---

## 19. Useful Tools

- **React DevTools** (browser extension)
- **ESLint** (with React plugin)
- **Prettier** (code formatting)

---

## 20. Frequently Asked Questions (FAQs)

**Q: Do I need to use Redux or Context for state management?**  
A: Only for advanced cases. Start with component state, lift state up, then try Context. Use Redux for very large apps.

**Q: Can I use TypeScript with React?**  
A: Yes! Highly recommended for large projects.

**Q: How do I deploy a React app?**  
A: You can use Vercel, Netlify, GitHub Pages, or your own server.

---

## 21. Practice and Learn!

The best way to learn React is by building small projects:
- To-do list
- Calculator
- Weather app
- Blog

---

Feel free to ask for examples, code reviews, or deeper dives into any topic!
