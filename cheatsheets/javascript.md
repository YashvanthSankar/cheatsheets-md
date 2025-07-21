# 🚀 JavaScript Cheatsheet

---

## 1. JavaScript: The Web’s Programming Language

JavaScript makes web pages interactive and dynamic.  
It runs in the browser (and also on servers via Node.js).

- **Why it’s hard?**  
  JavaScript mixes concepts from many languages, has tricky behaviors, and also interacts with the web page (DOM).
- **How to get better?**  
  Practice small pieces. Read code, try examples, and break things to see what happens!

---

## 2. Basics

| Concept    | Example                           | Notes                             |
|------------|-----------------------------------|-----------------------------------|
| Variable   | `let a = 3;`<br>`const pi = 3.14;`| Use `let` for changeable, `const` for constants. Prefer `const` unless variable will change. |
| Comment    | `// single-line`<br>`/* multi */` | Use comments to explain code.     |
| Output     | `console.log("Hello!");`          | Print to the console for debugging.|

### **Tips:**
- Use `const` unless you plan to change the value.
- Use `console.log()` often to see what’s happening.

---

## 3. Data Types

- **Number:** `let age = 21;`
- **String:** `let name = "Sara";`
- **Boolean:** `let isCool = true;`
- **Undefined:** Declared but not assigned (`let x;`)
- **Null:** Intentionally empty (`let y = null;`)
- **Array:** `let fruits = ["apple", "banana"];`
- **Object:** 
  ```js
  let user = { name: "Sara", age: 21 };
  ```

### **Tips:**
- Arrays are for lists, objects are for grouped data.
- Use `typeof` to check types.

---

## 4. Operators

| Operator      | Example         | Meaning           |
|---------------|----------------|-------------------|
| Add           | `a + b`        | Addition          |
| Subtract      | `a - b`        | Subtraction       |
| Multiply      | `a * b`        | Multiplication    |
| Divide        | `a / b`        | Division          |
| Modulo        | `a % b`        | Remainder         |
| Assignment    | `x = 5`        | Assign value      |
| Increment     | `x++`          | Add 1             |
| Decrement     | `x--`          | Subtract 1        |
| Compare       | `==`, `===`    | Equal, Strict Equal|
| Not           | `!=`, `!==`    | Not equal         |
| Greater/Less  | `>`, `<`, `>=`, `<=` | Compare   |
| And           | `&&`           | Both true         |
| Or            | `||`           | Either true       |
| Not           | `!true`        | Negate            |

### **Tips:**
- Use `===` (strict equal) to avoid surprise type conversions.
- Compare types carefully—`"5" == 5` is true, but `"5" === 5` is false.

---

## 5. Conditionals

```js
if (score > 50) {
  console.log("Passed!");
} else if (score == 50) {
  console.log("On the edge!");
} else {
  console.log("Failed!");
}
```

- **Ternary operator:**
  ```js
  let result = score > 50 ? "Passed" : "Failed";
  ```

- **Switch:**
  ```js
  switch(day) {
    case "Mon": console.log("Monday"); break;
    default: console.log("Other day");
  }
  ```

### **Tips:**
- Always use braces `{}` for multi-line blocks.
- Ternary is for quick one-line conditions.

---

## 6. Functions

```js
function greet(name) {
  return "Hello " + name;
}

const sayHi = (name) => `Hi ${name}`; // Arrow function
```

### **Tips:**
- Functions break problems into reusable steps.
- Arrow functions are concise, but behave differently with `this`.

---

## 7. Arrays

```js
let arr = [1, 2, 3];
arr.push(4);      // Add
arr.pop();        // Remove last
arr[0];           // First element
arr.length;       // Array size

// Loop through
arr.forEach(x => console.log(x));

// Transform
let doubled = arr.map(x => x*2); // [2,4,6]
```

### **Common Array Methods:**
- `push`, `pop`, `shift`, `unshift`
- `map`, `filter`, `reduce`, `find`, `forEach`, `some`, `every`, `includes`, `indexOf`

### **Tips:**
- Use `map` to transform, `filter` to keep some elements.
- Practice chaining methods for complex logic.

---

## 8. Objects

```js
let person = { name: "Ava", age: 20 };
console.log(person.name);
person.job = "Dev";
delete person.age;
```

- **Loop over properties:**
  ```js
  for (let key in person) {
    console.log(key, person[key]);
  }
  ```

### **Tips:**
- Keys are always strings.
- Use dot notation for known keys, bracket notation for dynamic keys.

---

## 9. Loops

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}

let i = 0;
while (i < 5) {
  i++;
}
```

- **for...of (arrays):**
  ```js
  for (let val of arr) { console.log(val); }
  ```
- **for...in (objects):**
  ```js
  for (let key in obj) { console.log(key); }
  ```

### **Tips:**
- Use `for...of` for arrays, `for...in` for objects.

---

## 10. String Methods

| Method           | Example                   | Result / Use                   |
|------------------|--------------------------|--------------------------------|
| `.length`        | `"abc".length`           | `3`                            |
| `.toUpperCase()` | `"hi".toUpperCase()`     | `"HI"`                         |
| `.substring()`   | `"hello".substring(0,3)` | `"hel"`                        |
| `.includes()`    | `"cat".includes("a")`    | `true`                         |
| `.replace()`     | `"hi".replace("h","b")`  | `"bi"`                         |
| `.split()`       | `"a,b,c".split(",")`     | `["a","b","c"]`                |
| `.trim()`        | `" hi ".trim()`          | `"hi"`                         |

### **Tips:**
- Strings are immutable—methods return new strings.
- Use template strings (`` `Hello ${name}` ``) for easy variable insertion.

---

## 11. Math

```js
Math.random();        // 0..1 random
Math.floor(3.7);      // 3
Math.ceil(3.1);       // 4
Math.round(3.5);      // 4
Math.max(2,5,1);      // 5
Math.min(2,5,1);      // 1
```

### **Tips:**
- `Math.random()` gives a number between 0 and 1. Multiply for a range.

---

## 12. Dates

```js
let now = new Date();
now.getFullYear();    // 2025
now.getMonth();       // 0 = Jan, 11 = Dec
now.getDate();        // day of month
now.toLocaleDateString(); // "7/21/2025"
```

### **Tips:**
- Months are zero-indexed!
- Use libraries like Day.js for advanced date handling.

---

## 13. DOM Manipulation (in browser)

```js
document.getElementById("id");
document.querySelector(".class");
document.querySelectorAll("li");

document.getElementById("id").innerText = "Yo!";
document.getElementById("id").style.color = "red";
```

**Create and Add Element:**
```js
let el = document.createElement("div");
el.textContent = "Hello";
document.body.appendChild(el);
```

### **Tips:**
- The DOM lets you change what’s displayed on the page.
- Always check if elements exist before changing them.

---

## 14. Events

```js
document.getElementById("btn").addEventListener("click", function() {
  alert("Button clicked!");
});
```

### **Tips:**
- Use arrow functions for simple event handlers.
- Learn about event bubbling and delegation for advanced UI.

---

## 15. JSON

```js
let obj = { a: 1 };
let str = JSON.stringify(obj); // '{"a":1}'
let obj2 = JSON.parse(str);    // { a: 1 }
```

### **Tips:**
- JSON is for exchanging data with servers/APIs.
- Always parse JSON before using it.

---

## 16. ES6+ Features

- **Arrow Functions:** `const f = x => x+1;`
- **Destructuring:**
  ```js
  let [a, b] = [1, 2];
  let {name, age} = person;
  ```
- **Spread/Rest:**
  ```js
  let arr2 = [...arr, 4, 5];
  function sum(...nums) { return nums.reduce((a,b) => a+b); }
  ```
- **Template Literals:**
  ```js
  let msg = `Hi, ${name}!`;
  ```
- **Default Parameters:**
  ```js
  function greet(name="friend") { ... }
  ```
- **Classes:**
  ```js
  class Animal {
    constructor(name) { this.name = name; }
    speak() { console.log(this.name); }
  }
  ```
- **Modules:**  
  Use `export`/`import` (in separate files) for modular code.

### **Tips:**
- Use destructuring for cleaner code.
- Use spread/rest for flexible parameter and array handling.
- Read about `this` in arrow functions vs regular functions.

---

## 17. Promises & Async/Await

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

### **Tips:**
- Use async/await for readable asynchronous code.
- Always use `try/catch` with async/await to handle errors.

---

## 18. Error Handling

```js
try {
  throw new Error("Oops!");
} catch (e) {
  console.log(e.message);
} finally {
  // always runs
}
```

### **Tips:**
- Always handle possible errors from APIs, DOM, etc.
- Use debugging tools and `console.log` to trace issues.

---

## 19. Useful Console Methods

```js
console.log("Normal log");
console.error("Error");
console.warn("Warning");
console.table([{a:1},{a:2}]);
console.time("label");
console.timeEnd("label");
```

---

## 20. How to Get Better at JavaScript

### **1. Practice Regularly**
- Write code every day, even small snippets.
- Try to solve simple problems like reversing a string, finding max in array, etc.

### **2. Read and Debug Code**
- Read others’ code (GitHub, StackOverflow).
- Debug errors instead of just copying solutions.

### **3. Build Real Projects**
- Start small: calculator, to-do list, quiz app.
- Gradually add features and complexity.

### **4. Use Online Resources**
- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info](https://javascript.info/)
- [freeCodeCamp JS](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

### **5. Learn the Concepts, Not Just Syntax**
- Understand how data flows, how scope and closures work, how asynchronous code works.
- Watch YouTube tutorials for visuals.

### **6. Ask for Help**
- Join coding communities: Discord, StackOverflow, Reddit.

### **7. Don’t Fear Mistakes**
- Errors are your guide—read them, Google them, and learn from them.

---

**🚩 Key Takeaways:**
- Learn JavaScript step by step. Don’t rush.
- Write, break, and fix code.
- Use `console.log` everywhere to “see” what’s going on.
- Build projects, even if they are tiny.
- Practice, patience, and curiosity = success!

---

**Happy Coding! 🌟**