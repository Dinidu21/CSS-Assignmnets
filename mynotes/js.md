## ❖ JavaScript

### 1. **What is JavaScript?**

JavaScript is a **high-level, interpreted scripting language** primarily used to add interactivity and dynamic behavior to web pages. It runs in the browser (and on servers via Node.js), manipulating the HTML/CSS, handling events, and communicating with servers.

* **Client-side**: Form validation, animations, AJAX calls.
* **Server-side** (Node.js): Building APIs, real-time apps.

**Follow-up Questions:**

* How does JavaScript differ from Java?
* What are modern JavaScript runtimes besides browsers?

---

### 2. **Explain the history of JavaScript**

* **1995**: Created by Brendan Eich at Netscape in just 10 days. Initially named **Mocha**, then **LiveScript**, finally **JavaScript**.
* **1996**: Standardized as **ECMAScript** by Ecma International.
* **2009**: ECMAScript 5 (ES5) brought strict mode, JSON support.
* **2015**: ECMAScript 6 (ES6/ES2015) introduced classes, modules, arrow functions, `let`/`const`.
* **Since 2016**: Annual updates (ES2016, ES2017…) adding async/await, optional chaining, BigInt, etc.

**Follow-up Questions:**

* What motivated the creation of JavaScript in just 10 days?
* How has the language evolved since ES6?

---

### 3. **What is ECMAScript?**

**ECMAScript** (often abbreviated ES) is the **specification** that standardizes JavaScript’s syntax, semantics, and APIs. JavaScript engines (V8, SpiderMonkey, Chakra) implement this spec.

* **Versions**: ES5, ES6 (ES2015), ES2016…ES2024.
* **Features**: Modules, classes, promises, async/await, new built-ins.

**Follow-up Questions:**

* What’s the difference between ES6 and “vanilla” JavaScript?
* How do transpilers like Babel relate to ECMAScript versions?

---

### 4. **What are the rules for creating valid identifiers in JS?**

Identifiers (variable, function, property names) must follow:

1. **Start** with a letter (A–Z, a–z), underscore (`_`), or dollar sign (`$`).
2. **Subsequent** characters can be letters, digits (0–9), `_`, or `$`.
3. **Cannot** be a reserved word (`if`, `for`, `class`, etc.).
4. **Case-sensitive**: `myVar` ≠ `MyVar`.

```js
let _count = 1;
const $price = 9.99;
function calculateTotal() { /* … */ }
```

**Follow-up Questions:**

* Are Unicode characters allowed in identifiers?
* How do reserved words evolve with new ES versions?

---

### 5. **What is the difference between `var`, `let`, and `const`?**

| Feature            | `var`                                | `let`                           | `const`                         |
| ------------------ | ------------------------------------ | ------------------------------- | ------------------------------- |
| **Scope**          | Function-scoped                      | Block-scoped                    | Block-scoped                    |
| **Hoisting**       | Hoisted + initialized to `undefined` | Hoisted but uninitialized (TDZ) | Hoisted but uninitialized (TDZ) |
| **Re-declaration** | Allowed in same scope                | Not allowed                     | Not allowed                     |
| **Reassignment**   | Allowed                              | Allowed                         | **Not** allowed                 |

```js
{
  var a = 1;    // visible outside block
  let b = 2;    // block-scoped
  const c = 3;  // block-scoped, read-only
}
console.log(a); // 1
console.log(b); // ReferenceError
```

**Follow-up Questions:**

* What is the Temporal Dead Zone (TDZ)?
* When should you prefer `const` over `let`?

---

### 6. **Why is JS known as a dynamic-type language?**

In JavaScript, **variables don’t have fixed types**. You can assign a value of any type at runtime:

```js
let data = 42;         // number
data = "hello";        // now a string
data = { x: 1, y: 2 }; // now an object
```

* **Type checks** happen at runtime.
* Promotes rapid development, but can lead to type-related bugs.

**Follow-up Questions:**

* How can TypeScript help with static typing?
* What runtime errors occur due to dynamic typing?

---

### 7. **Why was JS a loosely-typed language?**

“Loosely-typed” means **type conversions happen implicitly**:

```js
"5" - 2    // 3   (string → number)
"5" + 2    // "52" (number → string)
```

* JS performs coercion to match operations.
* Simplifies certain tasks but can introduce unexpected results.

**Follow-up Questions:**

* What are common pitfalls with type coercion?
* How do `==` vs. `===` relate to loose typing?

---

### 8. **What is variable hoisting?**

Hoisting is JavaScript’s behavior of **moving variable and function declarations to the top** of their containing scope before execution.

* **`var`** declarations are hoisted and initialized to `undefined`.
* **`let`/`const`** declarations are hoisted but not initialized (TDZ).
* **Function declarations** are hoisted with their body.

```js
console.log(x); // undefined (due to var hoisting)
var x = 5;

console.log(y); // ReferenceError (TDZ for let)
let y = 10;

foo();          // works
function foo() { console.log("called"); }
```

**Follow-up Questions:**

* How does hoisting differ in modules (strict mode)?
* Can you disable hoisting?

---

### 9. **What are the two ways of creating an array in JS?**

1. **Array literal** (recommended):

   ```js
   const fruits = ["apple", "banana", "cherry"];
   ```
2. **`Array` constructor**:

   ```js
   const numbers = new Array(1, 2, 3);
   // or new Array(3) creates [ <3 empty items> ]
   ```

**Follow-up Questions:**

* What pitfalls exist with `new Array(5)`?
* How do you create multi-dimensional arrays?

---

### 10. **When should we use `indexOf` on arrays and how does it work?**

* **Purpose:** Find the **first index** of a given element, or `-1` if not found.
* **Syntax:** `arr.indexOf(searchElement[, fromIndex])`.
* **Use-case:** Check existence before adding/removing items.

```js
const colors = ["red", "green", "blue"];
console.log(colors.indexOf("green"));  // 1
console.log(colors.indexOf("purple")); // -1
```

**Follow-up Questions:**

* How does `indexOf` handle objects (by reference)?
* What’s the difference between `indexOf` and `includes`?

---

### 11. **What methods can manipulate data in JS arrays?**

Common mutator methods (change the array):

* `push(...items)` – add to end
* `pop()` – remove from end
* `shift()` – remove from front
* `unshift(...items)` – add to front
* `splice(start, deleteCount, ...items)` – add/remove at arbitrary position
* `sort([compareFn])` – sort in place
* `reverse()` – reverse in place

Accessor methods (return new data, don’t mutate):

* `slice(start, end)` – shallow copy
* `concat(...arrays)` – merge arrays
* `map(fn)`, `filter(fn)`, `reduce(fn[, init])`, `forEach(fn)`, `find(fn)`, `findIndex(fn)`

**Follow-up Questions:**

* When use `map` vs. `forEach`?
* How do you remove a specific element by value?

---

### 12. **How to add a value to the last index of an array?**

* **`push` method**:

  ```js
  arr.push(value);
  ```
* **Direct assignment**:

  ```js
  arr[arr.length] = value;
  ```

`push` is preferred since it’s explicit and returns the new length.

**Follow-up Questions:**

* How to add multiple values at once?
* What’s the time complexity of `push`?

---

### 13. **What string-related methods do you know?**

Key methods on `String.prototype`:

* `charAt(index)`, `charCodeAt(index)`
* `concat(...strings)`
* `includes(substring)`, `startsWith()`, `endsWith()`
* `indexOf(substring)`, `lastIndexOf()`
* `slice(start, end)`, `substring(start, end)`, `substr(start, length)`
* `toUpperCase()`, `toLowerCase()`
* `trim()`, `trimStart()`, `trimEnd()`
* `split(separator[, limit])`
* `replace(searchValue, newValue)` (and regex variants)
* `repeat(count)`
* Template literals: `` `Hello ${name}` ``

**Follow-up Questions:**

* How do you escape backticks in template literals?
* What’s the difference between `slice` and `substring`?

---

### 14. **What are the data types in JS?**

JavaScript has **seven primitive** types and one object type:

* **Primitive**

  1. `string`
  2. `number`
  3. `bigint`
  4. `boolean`
  5. `undefined`
  6. `symbol`
  7. `null`
* **Object**

  * Everything else (arrays, functions, objects, dates, etc.)

**Follow-up Questions:**

* How does `typeof` treat `null`?
* When use `Symbol`?

---

### 15. **What is `BigInt`?**

`BigInt` is a numeric primitive for **arbitrarily large integers** beyond the safe integer limit (`±2^53−1`).

```js
const big = 9007199254740991n; // note the trailing 'n'
const sum = big + 1n;          // 9007199254740992n
```

* Operations must mix only `BigInt` with `BigInt` (no mixing with `number`).

**Follow-up Questions:**

* Why can’t you mix `BigInt` and `number` directly?
* What’s a use-case for BigInt?

---

### 16. **What is the difference between `null` and `undefined`?**

* **`undefined`**

  * Default value for **uninitialized** variables or missing object properties.
  * Returned by functions with no `return`.
* **`null`**

  * **Explicitly** assigned to represent “no value” or “empty”.

```js
let a;            // a is undefined
let b = null;     // b is explicitly “no value”
```

**Follow-up Questions:**

* How does `==` vs. `===` treat `null` and `undefined`?
* When should you use `null` over `undefined`?

---

### 17. **What is the DOM? Explain.**

The **Document Object Model** is a **tree representation** of an HTML (or XML) document. Each node represents elements, attributes, or text.

* **APIs** allow scripts to:

  * Query elements (`getElementById`, `querySelector`)
  * Modify structure (create, append, remove nodes)
  * Change styles and attributes
  * Listen for events

**Follow-up Questions:**

* What’s the difference between the HTMLCollection and NodeList?
* How do you optimize frequent DOM manipulations?

---

### 18. **What is the difference between `for…in` and `for…of`?**

* **`for…in`**

  * Iterates **enumerable property keys** (object’s own and inherited).

  ```js
  for (let key in obj) { … }
  ```
* **`for…of`**

  * Iterates **iterable values** (arrays, strings, Maps, Sets).

  ```js
  for (let value of array) { … }
  ```

```js
const arr = [10, 20, 30];
for (let i in arr)    console.log(i);     // “0”, “1”, “2”
for (let val of arr)  console.log(val);   // 10, 20, 30
```

**Follow-up Questions:**

* Can you use `for…of` on objects?
* How do you iterate keys and values together on a Map?

---

### 19. **What are literals and what is a literal-base object?**

* **Literals** are **syntax shortcuts** for creating values:

  * Number: `42`
  * String: `"hello"`, `` `world` ``
  * Boolean: `true`, `false`
  * Array: `[1, 2, 3]`
  * Object: `{ x: 1, y: 2 }`
  * RegExp: `/ab+c/`
* A **literal-based object** simply refers to the instance created by that literal notation (e.g., the object created by `{}`).

**Follow-up Questions:**

* What’s the difference between `new Object()` and `{}`?
* How do you create a RegExp literal and why use it?

---

### 20. **What are the two types of functions in JS? Explain with examples.**

1. **Function Declaration**

   ```js
   function greet(name) {
     return `Hello, ${name}!`;
   }
   ```

   * Hoisted with definition.
2. **Function Expression**

   ```js
   const add = function(x, y) {
     return x + y;
   };
   ```

   * Not hoisted; can be anonymous or named.
3. **Arrow Function** (ES6, variant of expression)

   ```js
   const square = n => n * n;
   ```

**Follow-up Questions:**

* How do `this` bindings differ between declarations, expressions, and arrows?
* When to use named function expressions?

---

### 21. **What is an event object? Explain.**

When a browser event occurs (click, keypress, etc.), the handler receives an **Event object** containing details:

* **`type`**: event type (`"click"`)
* **`target`**: element that triggered it
* **`currentTarget`**: element listener is attached to
* **Coordinates**, **keys pressed**, **defaultPrevented**, methods like `preventDefault()`, `stopPropagation()`

```js
button.addEventListener("click", function(event) {
  console.log(event.type, event.target);
  event.preventDefault();
});
```

**Follow-up Questions:**

* What’s the difference between `event.target` and `event.currentTarget`?
* How do synthetic events in React differ?

---

### 22. **What is jQuery?**

jQuery is a **lightweight, “write less, do more”** JavaScript library that simplifies:

* DOM traversal/manipulation
* Event handling
* AJAX requests
* Animation effects

```js
// Select all paragraphs, hide them
$("p").hide();

// AJAX GET
$.get("/api/data", data => console.log(data));
```

**Follow-up Questions:**

* Why did jQuery gain popularity?
* How do you include jQuery in a project today?

---

### 23. **What are the benefits of using jQuery?**

* **Cross-browser compatibility**: abstracts away differences.
* **Concise syntax**: powerful selectors and chaining.
* **Rich plugin ecosystem**.
* **Built-in AJAX and animation utilities**.
* **Ease of learning** for newcomers.

**Follow-up Questions:**

* Is jQuery still relevant in modern SPAs?
* What native APIs replace jQuery’s most-used features?

---

### 24. **What traversing methods have you used in jQuery and when?**

Common methods:

* **`.parent()`, `.parents()`** – move up the DOM.
* **`.children()`** – select direct children.
* **`.find(selector)`** – search descendants.
* **`.siblings()`** – select siblings.
* **`.next()`, `.prev()`** – adjacent elements.
* **`.closest(selector)`** – nearest ancestor matching selector.

Use these to **narrow** or **relocate** selections before manipulating or filtering nodes.

```js
// From a clicked button, find its containing .card
$(button).closest(".card").addClass("highlight");
```

**Follow-up Questions:**

* How do traversals differ in native DOM APIs?
* What’s the performance impact of deep traversals?

---

### 25. **Why was JS designed to have first-class functions?**

First-class functions mean **functions are treated like any other value**:

* Passed as arguments
* Returned from other functions
* Assigned to variables or object properties

This enables powerful patterns:

* **Callbacks**
* **Higher-order functions** (`map`, `filter`, `reduce`)
* **Function factories** / currying
* **Event handlers**

```js
function makeMultiplier(x) {
  return function(y) {
    return x * y;
  };
}
const double  = makeMultiplier(2);
console.log(double(5)); // 10
```

**Follow-up Questions:**

* What is a higher-order function?
* How do you implement function currying in JS?

---
