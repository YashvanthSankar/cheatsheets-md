# React Router

---

## 1. What is React Router?

React Router is a popular library for handling navigation (routing) in React apps.  
It lets you switch between different "pages" (components) without reloading the browser.

---

## 2. Installation

```bash
npm install react-router-dom
```
---

## 3. Basic Setup & Example

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function Home() {
  return <h2>Home Page</h2>;
}
function About() {
  return <h2>About Page</h2>;
}
function NotFound() {
  return <h2>404 Not Found</h2>;
}

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```
**Explanation:**  
- `<BrowserRouter>`: Wraps your app to enable routing.
- `<Routes>`: Container for all route definitions.
- `<Route>`: Defines a path and the component to show.
- `"*"` path: Catches all undefined routes (404).

---

## 4. Navigation Links

```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```
**Tip:**  
Use `<Link>` instead of `<a>` to avoid page reloads.

---

## 5. Programmatic Navigation

```jsx
import { useNavigate } from "react-router-dom";

function MyButton() {
  const navigate = useNavigate();
  return (
    <button onClick={() => navigate("/about")}>Go to About</button>
  );
}
```
**Explanation:**  
Use `useNavigate()` to change pages from code (e.g., after a form submit).

---

## 6. URL Parameters (Dynamic Routes)

```jsx
// In App.js
<Route path="/users/:id" element={<User />} />

// In User.js
import { useParams } from "react-router-dom";

function User() {
  const { id } = useParams();
  return <div>User ID: {id}</div>;
}
```
**Explanation:**  
`:id` in the path lets you match URLs like `/users/123`.  
`useParams()` lets you read the value.

---

## 7. Query Strings

```jsx
// URL: /search?term=react
import { useSearchParams } from "react-router-dom";

function SearchPage() {
  const [searchParams] = useSearchParams();
  const term = searchParams.get("term");
  return <div>Searching for: {term}</div>;
}
```
**Explanation:**  
Read query strings (the part after `?`) with `useSearchParams`.

---

## 8. Nested Routes Example

```jsx
// In App.js
<Route path="/dashboard/*" element={<Dashboard />} />

// In Dashboard.js
import { Routes, Route, Link } from "react-router-dom";
function Stats() { return <div>Stats</div>; }
function Settings() { return <div>Settings</div>; }

function Dashboard() {
  return (
    <div>
      <Link to="stats">Stats</Link>
      <Link to="settings">Settings</Link>
      <Routes>
        <Route path="stats" element={<Stats />} />
        <Route path="settings" element={<Settings />} />
      </Routes>
    </div>
  );
}
```
**Explanation:**  
Nested routes let you show sub-pages inside a parent page.

---

## 9. Redirects

```jsx
import { Navigate } from "react-router-dom";

// In your routes:
<Route path="/old" element={<Navigate to="/new" replace />} />
```
**Explanation:**  
Use `<Navigate>` to redirect users from one route to another.

---

## 10. Route Protection (Private Routes)

```jsx
import { Navigate } from "react-router-dom";

function PrivateRoute({ children }) {
  const isAuth = /* check if logged in */;
  return isAuth ? children : <Navigate to="/login" />;
}

// Usage:
<Route path="/dashboard" element={
  <PrivateRoute>
    <Dashboard />
  </PrivateRoute>
} />
```
**Explanation:**  
Protect routes so only logged-in users can access them.

---

## 11. Outlet (for Nested Routes)

```jsx
import { Outlet } from "react-router-dom";

function Layout() {
  return (
    <div>
      <Header />
      <Outlet /> {/* Renders child routes here */}
      <Footer />
    </div>
  );
}

// In your routes:
<Route path="/" element={<Layout />}>
  <Route index element={<Home />} />
  <Route path="about" element={<About />} />
</Route>
```
**Explanation:**  
`<Outlet />` renders nested route components in the parent layout.

---

## 12. Not Found Route (404 Page)

```jsx
<Route path="*" element={<NotFound />} />
```
**Explanation:**  
The `*` path matches any unmatched route (shows a custom 404 page).

---

## 13. Useful React Router Hooks

| Hook              | Usage                                      |
|-------------------|--------------------------------------------|
| `useNavigate()`   | Go to a route programmatically             |
| `useParams()`     | Get URL parameters                         |
| `useSearchParams()`| Get/set query string params                |
| `useLocation()`   | Info about current URL                     |
| `useMatch()`      | Match current URL against pattern          |

---

## 14. Example: Full Simple App

```jsx
import { BrowserRouter, Routes, Route, Link, useParams } from "react-router-dom";

function Home() { return <h2>Home</h2>; }
function About() { return <h2>About</h2>; }
function User() {
  const { id } = useParams();
  return <h2>User ID: {id}</h2>;
}
function NotFound() { return <h2>404 Not Found</h2>; }

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>{" | "}
        <Link to="/about">About</Link>{" | "}
        <Link to="/users/42">User 42</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users/:id" element={<User />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 15. Resources

- [React Router Docs](https://reactrouter.com/en/main)
- [React Router Tutorial](https://reactrouter.com/en/main/start/tutorial)
- [FreeCodeCamp React Router Guide](https://www.freecodecamp.org/news/react-router-in-5-minutes/)

---

**Happy Routing! 🚦**
