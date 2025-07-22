# React Context

## What is React Context?

- **Context** lets you share data (state) across many components, without having to pass props down manually at every level.
- Useful for "global" data: user info, theme, language, etc.

---

## When to Use Context

- When some data needs to be accessible by many components at different nesting levels.
- Not a replacement for all state or for libraries like Redux in complex cases.

---

## How Context Works: The Three Steps

### 1. Create Context

```jsx
import React from 'react';

const MyContext = React.createContext(defaultValue);
```
- `defaultValue` is used only if a component does not have a matching provider above it.

---

### 2. Provide Context

Wrap part of your component tree with a **Provider**.

```jsx
<MyContext.Provider value={/* some value */}>
  {/* children that need the context */}
</MyContext.Provider>
```

---

### 3. Consume Context

There are two ways:

#### a) Using `useContext` (Function Components – Recommended)

```jsx
import React, { useContext } from 'react';

const value = useContext(MyContext);
```

#### b) Using `Context.Consumer` (Older)

```jsx
<MyContext.Consumer>
  {value => /* render something based on the context value */}
</MyContext.Consumer>
```

---

## Complete Example

Let’s create a theme context to change between light and dark mode.

```jsx
// ThemeContext.js
import React, { createContext, useState, useContext } from 'react';

// 1. Create Context
const ThemeContext = createContext();

// 2. Create a Provider component
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  const toggleTheme = () => setTheme(t => (t === 'light' ? 'dark' : 'light'));

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// 3. Custom hook for easier usage
export function useTheme() {
  return useContext(ThemeContext);
}
```

**Usage in your App:**

```jsx
// App.js
import React from 'react';
import { ThemeProvider, useTheme } from './ThemeContext';

function ThemeButton() {
  const { theme, toggleTheme } = useTheme();
  return (
    <button onClick={toggleTheme}>
      Current theme: {theme}
    </button>
  );
}

function App() {
  return (
    <ThemeProvider>
      <ThemeButton />
      {/* other components */}
    </ThemeProvider>
  );
}

export default App;
```

---

## Best Practices

- Don’t overuse Context – for deeply nested or widely used data only.
- For performance, avoid putting frequently changing values in Context (it causes all consumers to re-render).
- For large apps, split global state into multiple contexts (e.g., AuthContext, ThemeContext).
- Create custom hooks (like `useTheme`) to make consuming context easier.

---

## Common Use Cases

- Theme switching (dark/light)
- Authentication (user info, login status)
- Language/i18n
- App settings

---

## Further Reading

- [React Context Docs](https://react.dev/reference/react/useContext)
- [When to Use Context](https://react.dev/reference/react/useContext#alternatives)

---

**Summary:**  
React Context is a powerful tool for sharing state/data across your app without prop-drilling. Use it for data that’s truly global, and combine with hooks for clean, maintainable code.
