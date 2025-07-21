# Complete JavaScript Cheatsheet 

---

## 1. What is JavaScript?

JavaScript is the main programming language of the web.  
It lets you make web pages interactive—think buttons, forms, pop-ups, games, animations, and more.

- **Where does it run?**  
  - In the browser (Chrome, Firefox, Safari, etc.)
  - On servers (with Node.js)
- **Why learn it?**  
  - It’s essential for web development, and used everywhere.

---

## 2. Writing and Running JavaScript

- **In a web page:**  
  ```html
  <script>
    // Your JS code here
    console.log("Hello, world!");
  </script>
  ```
- **In the browser console:**  
  Open DevTools (F12 or right-click > Inspect > Console tab) and type JS code.

---

## 3. Variables and Data Types

Variables store data.  
Declare with `let`, `const`, or `var` (use `let` or `const` in modern JS).

```js
let age = 18;           // Number
const name = "Sara";    // String
let isHappy = true;     // Boolean
let nothing = null;     // Null (empty)
let notSet;             // Undefined
let colors = ["red", "green"]; // Array (list)
let person = { name: "Sara", age: 18 }; // Object
```

**Explanation:**  
- `let` is for variables you can change.
- `const` is for values that stay the same.
- Strings use quotes (`"text"`).
- Arrays are lists (`[1,2,3]`).
- Objects are key-value groups (`{key: value}`).

---

## 4. Operators

Do math, compare values, and combine things.

| Operator      | Example         | Meaning                   |
|---------------|----------------|---------------------------|
| Add           | `a + b`        | Addition or string join   |
| Subtract      | `a - b`        | Subtraction               |
| Multiply      | `a * b`        | Multiplication            |
| Divide        | `a / b`        | Division                  |
| Remainder     | `a % b`        | Modulo (remainder)        |
| Assignment    | `x = 5`        | Set value                 |
| Increment     | `x++`          | Add 1                     |
| Decrement     | `x--`          | Subtract 1                |
| Compare       | `==`, `===`    | Equal (`===` is strict)   |
| Not           | `!=`, `!==`    | Not equal                 |
| Greater/Less  | `>`, `<`, `>=`, `<=` | Comparison         |
| And           | `&&`           | Both must be true         |
| Or            | `||`           | Either must be true       |
| Not           | `!true`        | Opposite (false)          |

**Explanation:**  
- Use `===` for strict equality (checks type too).
- Strings can be joined with `+` (`"Hi " + name`).

---

## 5. Conditionals (If/Else & Switch)

Make decisions based on conditions.

```js
if (score >= 50) {
  console.log("Pass");
} else {
  console.log("Fail");
}
```

**Ternary operator (quick if/else):**
```js
let result = score >= 50 ? "Pass" : "Fail";
```

**Switch (multiple choices):**
```js
switch(day) {
  case "Monday":
    console.log("Start of week");
    break;
  case "Friday":
    console.log("Almost weekend");
    break;
  default:
    console.log("Regular day");
}
```

**Explanation:**  
- Use `if` for simple yes/no checks.
- Use `switch` for multiple options.

---

## 6. Functions

Reusable blocks of code.

```js
function greet(name) {
  return "Hello, " + name;
}

const double = x => x * 2; // Arrow function (ES6+)
```

**Parameters:** Values you pass to a function.  
**Return:** What the function gives back.

**Explanation:**  
- Use functions to avoid repeating code.
- Arrow functions are shorter and popular.

---

## 7. Arrays (Lists)

Store multiple values.

```js
const fruits = ["apple", "banana", "orange"];
console.log(fruits[0]); // "apple"

fruits.push("mango");   // Add to end
fruits.pop();           // Remove last
fruits.length;          // Number of items
```

**Common Methods:**
- `forEach`: Do something for each item.
  ```js
  fruits.forEach(fruit => console.log(fruit));
  ```
- `map`: Create new array with changed items.
  ```js
  const bigFruits = fruits.map(fruit => fruit.toUpperCase());
  ```
- `filter`: Keep some items.
  ```js
  const longFruits = fruits.filter(fruit => fruit.length > 5);
  ```
- `find`: Get first matching item.
  ```js
  const firstBanana = fruits.find(fruit => fruit == "banana");
  ```

**Explanation:**  
- Arrays are used for lists—shopping, scores, etc.
- Methods make working with arrays easy and powerful.

---

## 8. Objects

Group related data.

```js
const user = {
  name: "Sara",
  age: 18,
  isStudent: true
};

console.log(user.name); // "Sara"
user.city = "Delhi";    // Add property
delete user.age;        // Remove property
```

**Loop over properties:**
```js
for (let key in user) {
  console.log(key, user[key]);
}
```

**Explanation:**  
- Objects let you store data with labels.
- Use dot `user.name` or bracket `user["name"]` notation.

---

## 9. Loops

Repeat actions.

**For loop (counted):**
```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

**While loop (until something changes):**
```js
let n = 3;
while (n > 0) {
  console.log(n);
  n--;
}
```

**For...of (arrays):**
```js
for (let fruit of fruits) {
  console.log(fruit);
}
```

**For...in (objects):**
```js
for (let key in user) {
  console.log(key, user[key]);
}
```

**Explanation:**  
- Use loops to process lists or repeat steps.

---

## 10. Strings

Text data.

```js
let greeting = "Hello, world!";
greeting.length;                  // Number of characters
greeting.toUpperCase();           // "HELLO, WORLD!"
greeting.substring(0, 5);         // "Hello"
greeting.includes("world");       // true
greeting.replace("world", "JS");  // "Hello, JS!"
greeting.split(", ");             // ["Hello", "world!"]
greeting.trim();                  // "Hello, world!" (removes spaces at ends)
```

**Explanation:**  
- Strings are used for names, messages, etc.
- Many built-in methods for editing and checking strings.

---

## 11. Math

Built-in object for math operations.

```js
Math.random();        // Random number 0-1
Math.floor(2.9);      // 2 (round down)
Math.ceil(2.1);       // 3 (round up)
Math.round(2.5);      // 3 (nearest)
Math.max(1, 3, 2);    // 3
Math.min(1, 3, 2);    // 1
```

**Explanation:**  
- Math object is used for calculations, random numbers, rounding, and more.

---

## 12. Dates

Work with time and dates.

```js
const now = new Date();
now.getFullYear();         // 2025
now.getMonth();            // 0 = Jan, 11 = Dec
now.getDate();             // Day of month
now.toLocaleDateString();  // "7/21/2025"
```

**Explanation:**  
- Use Date for timestamps, deadlines, and more.
- Months start from 0 (January).

---

## 13. DOM Manipulation (Web Pages)

Change the page with JS (in browser).

```js
const title = document.getElementById("main-title");
title.innerText = "New Title";

const btn = document.querySelector(".btn");
btn.style.backgroundColor = "red";
```

**Create/Add Elements:**
```js
const div = document.createElement("div");
div.textContent = "Hello";
document.body.appendChild(div);
```

**Explanation:**  
- DOM is the page structure; JS can read and change it.
- Use `getElementById`, `querySelector`, etc. to pick elements.

---

## 14. Events

Respond to user actions.

```js
btn.addEventListener("click", () => {
  alert("Button clicked!");
});
```

**Explanation:**  
- Events let you react to clicks, typing, etc.
- Use `addEventListener` to run code when something happens.

---

## 15. JSON

Store and exchange data (with servers/APIs).

```js
const obj = { a: 1, b: 2 };
const str = JSON.stringify(obj); // Convert object to text
const obj2 = JSON.parse(str);    // Convert text back to object
```

**Explanation:**  
- JSON is a universal format for sending data (like a language everyone understands).

---

## 16. ES6+ Features

Modern JavaScript has many upgrades!

1. **Arrow Functions**
   ```js
   const add = (a, b) => a + b;
   ```

2. **Destructuring**
   ```js
   const [x, y] = [1, 2];
   const {name, age} = user;
   ```

3. **Spread/Rest**
   ```js
   const arr2 = [...fruits, "kiwi"];
   function sum(...nums) { return nums.reduce((a,b) => a+b); }
   ```

4. **Template Literals**
   ```js
   const greet = `Hello, ${name}!`;
   ```

5. **Default Parameters**
   ```js
   function greet(name = "friend") { ... }
   ```

6. **Classes**
   ```js
   class Animal {
     constructor(name) { this.name = name; }
     speak() { console.log(this.name); }
   }
   ```

7. **Modules**
   - Split code into files with `export` and `import`.

**Explanation:**  
- These features make code easier to write and understand.

---

## 17. Promises & Async/Await

Handle actions that take time (like fetching data).

**Promises:**
```js
function wait(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
wait(1000).then(() => console.log("Done!"));
```

**Async/Await:**
```js
async function go() {
  await wait(1000);
  console.log("Done!");
}
go();
```

**Explanation:**  
- Asynchronous code lets things happen in the background.
- Promises and `async/await` make it easier to read and write.

---

## 18. Error Handling

Catch and deal with problems so your app doesn’t crash.

```js
try {
  throw new Error("Something went wrong");
} catch (e) {
  console.log(e.message);
} finally {
  // Always runs
}
```

**Explanation:**  
- Use `try/catch` to handle bugs and errors gracefully.

---

## 19. Useful Console Methods

Debug and inspect your code.

```js
console.log("Normal log");
console.error("Error!");
console.warn("Warning!");
console.table([{a:1}, {a:2}]);
console.time("timer");
console.timeEnd("timer");
```

**Explanation:**  
- Console is your friend for debugging and checking values.

---

## 20. Scope and Closures

**Scope:** Where variables are available.

```js
let a = 1;
function show() {
  let b = 2;
  console.log(a); // 1
  console.log(b); // 2
}
console.log(b); // Error! b is only inside function
```

**Closure:** Function remembers variables where it was created.

```js
function outer() {
  let x = 10;
  function inner() {
    console.log(x); // 10
  }
  return inner;
}
const myFunc = outer();
myFunc(); // 10
```

**Explanation:**  
- Scope controls variable visibility.
- Closures let functions "remember" their environment.

---

## 21. Hoisting

JS moves variable/function declarations to the top of their scope before running code.

```js
console.log(a); // undefined
var a = 5;
```

**Explanation:**  
- With `var`, variables are "hoisted" but not initialized.
- `let` and `const` are NOT initialized and give errors if used before declaration.

---

## 22. Strict Mode

Catches common mistakes, makes code safer.

```js
"use strict";
x = 5; // Error! x not declared
```

**Explanation:**  
- Add `"use strict";` at the top of your file or function.

---

## 23. Useful Patterns and Tips

- **DRY:** Don’t Repeat Yourself. Use functions!
- **Read errors:** Errors help you fix bugs.
- **Practice:** Code every day, even small snippets.
- **Build projects:** Start simple (to-do app, calculator, quiz).
- **Ask for help:** Communities are friendly (StackOverflow, Discord, Reddit).

---

## 24. Resources

- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info](https://javascript.info/)
- [freeCodeCamp JS](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

---

## 25. Key Takeaways

- JavaScript lets you interact with web pages and build web apps.
- Learn step by step—variables, functions, loops, arrays, objects, DOM, and ES6+ features.
- Use the browser console to test ideas and debug.
- Practice, experiment, and have fun!

---

**Happy Coding! 🌟**