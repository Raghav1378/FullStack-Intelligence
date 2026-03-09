# The Ultimate JavaScript Master Guide

Welcome to the comprehensive guide on JavaScript. This document covers end-to-end concepts and syntax, designed to take you from basics to advanced topics.

---

## Part 1: Basics and Control Flow

### 1. Variables (`var`, `let`, `const`)
Variables store data. Modern JavaScript uses `let` and `const`.

*   **`var`**: Function-scoped, can be redeclared, hoisted with `undefined`. (Avoid using this in modern JS).
*   **`let`**: Block-scoped, can be updated but NOT redeclared in the same scope.
*   **`const`**: Block-scoped, cannot be updated or redeclared. Always use this unless you know the value will change.

```javascript
var oldWay = "I am old";
let changeable = "I can change";
const fixed = "I cannot change";

changeable = "New value"; // OK
// fixed = "New value"; // TypeError
```

### 2. Data Types
JavaScript is dynamically typed.

**Primitive Types:**
*   **String:** Text data. `"Hello"`, `'World'`, `` `Template literals ${changeable}` ``.
*   **Number:** Both integers and floating-point. `42`, `3.14`, `NaN` (Not a Number).
*   **BigInt:** For numbers beyond the safe integer limit. `9007199254740991n`.
*   **Boolean:** Logical entity. `true` or `false`.
*   **Undefined:** A variable that has been declared but not assigned a value.
*   **Null:** Intentional absence of any object value.
*   **Symbol:** Unique and immutable primitive used for object properties.

**Structural (Object) Types:**
*   **Object:** Key-value pairs. `{ name: "John", age: 30 }`.
*   **Array:** Ordered list. `[1, 2, 3, "four"]`.
*   **Function:** Callable object.

### 3. Type Conversion (Coercion vs Casting)
*   **Implicit (Coercion):** JavaScript automatically converts types.
    ```javascript
    "5" + 2 // "52" (String concatenation)
    "5" - 2 // 3 (Numeric subtraction)
    ```
*   **Explicit (Casting):** Manually converting types using `Number()`, `String()`, `Boolean()`.

### 4. Operators
*   **Arithmetic:** `+`, `-`, `*`, `/`, `%` (remainder), `**` (exponentiation).
*   **Assignment:** `=`, `+=`, `-=`, etc.
*   **Comparison:** 
    *   `==` (loose equality, converts type).
    *   `===` (strict equality, checks type and value - **always use this**).
    *   `!=`, `!==`, `>`, `<`, `>=`, `<=`.
*   **Logical:** `&&` (AND), `||` (OR), `!` (NOT).

### 5. Control Flow
**Conditional Statements:**
```javascript
let age = 18;

// if/else
if (age >= 18) {
    console.log("Adult");
} else if (age >= 13) {
    console.log("Teen");
} else {
    console.log("Child");
}

// switch (strict comparison)
let day = 2;
switch (day) {
    case 1: console.log("Monday"); break;
    case 2: console.log("Tuesday"); break;
    default: console.log("Unknown");
}

// Ternary Operator (Shorthand if/else)
let status = age >= 18 ? "Adult" : "Minor";
```

**Loops:**
```javascript
// for loop (when you know exact iterations)
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// while loop (when condition determines iterations)
let count = 0;
while (count < 5) {
    count++;
}

// do-while (runs AT LEAST once)
do {
    console.log(count);
} while (count > 10);
```

---

## Part 2: Functions and Scope

### 1. Function Declarations vs Expressions
```javascript
// Function Declaration (Hoisted)
function greet(name) {
    return `Hello, ${name}`;
}

// Function Expression (Not hoisted)
const greetExpr = function(name) {
    return `Hello, ${name}`;
};
```

### 2. Arrow Functions
A shorter syntax introduced in ES6. They do NOT have their own `this` context.
```javascript
// Traditional expression
const add = function(a, b) { return a + b; };

// Arrow function
const addArrow = (a, b) => a + b; // Implicit return

// Single parameter
const square = x => x * x;
```

### 3. Parameters (Default & Rest)
```javascript
// Default parameters
function multiply(a, b = 1) {
    return a * b; // If b is not passed, it defaults to 1
}

// Rest operator (Gathers remaining arguments into an array)
function sumAll(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}
sumAll(1, 2, 3, 4); // 10
```

### 4. Scope and Closures
*   **Lexical Scope:** Functions have access to variables declared in their outer scope.
*   **Closure:** A function that remembers its outer variables and can access them, even after the outer function has finished executing.

```javascript
function createCounter() {
    let count = 0; // 'count' is essentially private
    return function() {
        count++; // Inner function closes over 'count'
        return count;
    };
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

---

## Part 3: Objects, Arrays, and Modern Syntax

### 1. Objects
```javascript
const user = {
    name: "Alice",
    age: 25,
    greet() {
        console.log(`Hi, I'm ${this.name}`);
    }
};

// Accessing properties
console.log(user.name); // Dot notation
console.log(user["age"]); // Bracket notation
```

### 2. Arrays & Higher-Order Methods
Arrays have very powerful built-in methods.
```javascript
const numbers = [1, 2, 3, 4, 5];

// .map() - transforms every item and returns a NEW array
const doubled = numbers.map(num => num * 2);

// .filter() - returns a NEW array with items that pass the condition
const evens = numbers.filter(num => num % 2 === 0);

// .reduce() - accumulates values down to a single value
const sum = numbers.reduce((total, num) => total + num, 0);

// .forEach() - simple loop, returns undefined
numbers.forEach(num => console.log(num));
```

### 3. Destructuring
Extracting values from arrays or properties from objects into distinct variables.
```javascript
// Object Destructuring
const person = { first: "John", last: "Doe" };
const { first, last } = person;

// Array Destructuring
const colors = ["red", "green", "blue"];
const [primary, secondary] = colors;
```

### 4. Spread Operator (`...`)
Expands iterables into single elements. Very useful for copying or combining.
```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4]

const obj1 = { a: 1 };
const clone = { ...obj1, b: 2 }; // { a: 1, b: 2 }
```

### 5. Optional Chaining (`?.`) & Nullish Coalescing (`??`)
```javascript
// Optional Chaining: Safely access deeply nested properties without throwing errors
const profile = {};
console.log(profile.address?.city); // undefined, doesn't crash

// Nullish Coalescing: Provides a fallback if the value is strictly null or undefined
let input = null;
let name = input ?? "Guest"; // "Guest"
// Differs from || which falls back on any falsy value (e.g., '', 0, false)
```

---

## Part 4: Asynchronous JavaScript
JavaScript is single-threaded but handles asynchronous operations via the Event Loop.

### 1. Callbacks
Passing a function to be executed later. (Often leads to "Callback Hell" if deeply nested).
```javascript
setTimeout(() => {
    console.log("Executes after 1 second");
}, 1000);
```

### 2. Promises
Represents the eventual completion (or failure) of an asynchronous operation.
```javascript
const myPromise = new Promise((resolve, reject) => {
    let success = true;
    if (success) resolve("Data fetched!");
    else reject("Error occurred");
});

myPromise
    .then(data => console.log(data))
    .catch(error => console.error(error))
    .finally(() => console.log("Always runs"));
```

### 3. `async` / `await`
Syntactic sugar over Promises. Makes asynchronous code look synchronous and easier to read.
```javascript
async function fetchData() {
    try {
        // await pauses execution until the promise resolves
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Fetch failed", error);
    }
}
```

---

## Part 5: Object-Oriented JS, Modules, and Error Handling

### 1. `this` Keyword
The execution context.
*   **Global/Function scope (non-strict):** `window` (browser).
*   **Method:** The object the method is called on.
*   **Arrow Function:** Inherits `this` lexically from the surrounding scope.

### 2. Classes (ES6)
Syntactic sugar over JS's prototypical inheritance.
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} makes a noise.`);
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name); // Must call parent constructor
        this.breed = breed;
    }
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const rex = new Dog("Rex", "German Shepherd");
rex.speak(); // "Rex barks."
```

### 3. Modules (ES6 import/export)
Sharing code between files.
```javascript
// math.js
export const add = (a, b) => a + b;
export default function subtract(a, b) { return a - b; }

// app.js
import subtract, { add } from './math.js';
console.log(add(5, 2));
```

### 4. Error Handling (`try/catch`)
Prevent your app from crashing gracefully.
```javascript
try {
    // Code that might throw an error
    let a = undefinedVariable;
} catch (error) {
    console.log("An error was caught:", error.message);
} finally {
    console.log("Cleanup code runs regardless of error");
}

// Throwing custom errors
function validateAge(age) {
    if (age < 0) throw new Error("Age cannot be negative");
}
```
