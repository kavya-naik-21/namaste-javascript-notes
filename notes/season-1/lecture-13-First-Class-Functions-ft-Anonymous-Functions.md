# Episode 13 : First Class Functions ft. Anonymous Functions

> Functions are heart ♥ of Javascript.

### Q: What is Function statement?

Below way of creating function are function statement.

```js
function a() {
  console.log("Hello");
}
a(); // Hello
```

### Q: What is Function Expression?

Assigning a function to a variable. Function acts like a value.

```js
var b = function () {
  console.log("Hello");
};
b();
```

### Q: Difference between function statement and expression

The major difference between these two lies in **Hoisting**.

```js
a(); // "Hello A"
b(); // TypeError
function a() {
  console.log("Hello A");
}
var b = function () {
  console.log("Hello B");
};
// Why? During mem creation phase a is created in memory and function assigned to a. But b is created like a variable (b:undefined) and until code reaches the function()  part, it is still undefined. So it cannot be called.
```

### Q: What is Function Declaration?

Other name for **function statement**.

### Q: What is Anonymous Function?

A function without a name.

```js
function () {

}// this is going to throw Syntax Error - Function Statement requires function name.
```

- They don't have their own identity. So an anonymous function without code inside it results in an error.
- Anonymous functions are used when functions are used as values eg. the code sample for **function expression** above.
- in **function statements** cannot you cannot use anonymous functions

### Q: What is Named Function Expression?

Same as Function Expression but function has a name instead of being anonymous.

```js
var b = function xyz() {
  console.log("b called");
};
b(); // "b called"
xyz(); // Throws ReferenceError:xyz is not defined.
// xyz function is not created in global scope. So it can't be called.
```

### Q: Parameters vs Arguments?

```js
var b = function (param1, param2) {
  // labels/identifiers are parameters
  console.log("b called");
};
b(arg1, arg2); // arguments - values passed inside function call
```

### Q: What is First Class Function aka First Class Citizens?

We can pass functions inside a function as arguments and
/or return a function(HOF). These ability are altogether known as First class function. It is programming concept available in some other languages too.
- function can be passed as arguments
- function can be returned
- function can be assigned as value
- i.e, the ability to use functions as values is called first class functions - ie., passed as args and can be returned as well

```js
var b = function (param1) {
  console.log(param1); // prints " f() {} "
};
b(function () {});

// Other way of doing the same thing:
var b = function (param1) {
  console.log(param1);
};
function xyz() {}
b(xyz); // same thing as prev code

// we can return a function from a function:
var b = function (param1) {
  return function () {};
};
console.log(b()); //we log the entire fun within b.
```



# Function Definition vs Function Statement vs Function Declaration in JavaScript

## 1️⃣ Function Definition
A **function definition** refers to the entire syntax used to define a function, regardless of the way it is defined (declaration, expression, arrow function, etc.).

### Example:
```js
function greet() {
    console.log("Hello, World!");
}
```
- The entire function, including its name, parameters, and body, is the **function definition**.

### Memory Allocation:
- Function definitions are stored in memory differently depending on how they are declared:
  - **Function Declarations**: Stored in memory during the creation phase and hoisted, allowing usage before definition.
  - **Function Expressions & Arrow Functions**: Memory is allocated during execution, meaning they cannot be used before their assignment.

---

## 2️⃣ Function Declaration (Function Statement)
A **function declaration** (also called a **function statement**) defines a function using the `function` keyword without assigning it to a variable.

### Example:
```js
function sayHello() {
    console.log("Hello!");
}
```

### Key Characteristics:
✔ **Named function**  
✔ **Hoisted** (can be called before its definition)  
✔ Stored in memory during the creation phase  

### Memory Allocation:
- In the **memory creation phase**, JavaScript allocates memory for function declarations and stores the function entirely.
- Function declarations are **hoisted**, meaning they can be used before their definition.

#### Example of Hoisting:
```js
sayHello(); // ✅ Works due to hoisting

function sayHello() {
    console.log("Hello!");
}
```

---

## 3️⃣ Function Expression
A **function expression** is when a function is assigned to a variable.

### Example:
```js
const greet = function() {
    console.log("Hello, User!");
};
```

### Key Characteristics:
✔ **Anonymous function** (in most cases)  
✔ **Not hoisted** (Cannot be used before definition)  
✔ Stored in memory at runtime  

### Memory Allocation:
- During the **memory creation phase**, JavaScript allocates memory for the variable `greet`, but assigns it `undefined`.
- The function definition is stored in memory **only during execution**.

#### Example of Hoisting Issue:
```js
greet(); // ❌ Error: greet is not a function

const greet = function() {
    console.log("Hello!");
};
```
> The function is stored in memory **only when execution reaches this line**, not during the initial memory allocation phase.

---

## 4️⃣ Arrow Function (Function Expression)
Arrow functions are another form of **function expression** with a concise syntax.

### Example:
```js
const add = (a, b) => a + b;
```

### Memory Allocation:
- Like normal function expressions, arrow functions are **not hoisted**.
- They are assigned to variables and stored **only during execution**.

---

## 🔥 Summary Table
| Feature                | Function Declaration (Statement) | Function Expression | Arrow Function |
|------------------------|--------------------------------|----------------------|---------------|
| **Hoisting**           | ✅ Yes                         | ❌ No                 | ❌ No          |
| **Memory Allocation**  | Stored in memory in creation phase | Assigned at execution | Assigned at execution |
| **Usage before definition** | ✅ Allowed | ❌ Not allowed | ❌ Not allowed |
| **Anonymous**         | ❌ No (Has a name)             | ✅ Mostly anonymous (Named function expressions are also possible) | ✅ Always anonymous |
| **Syntax**            | `function name() {}`          | `const name = function() {}` | `const name = () => {}` |

---

## Final Takeaway
- **Function Declaration (Function Statement)**: Hoisted and stored in memory before execution.
- **Function Expression**: Assigned at execution, not hoisted.
- **Arrow Function**: Similar to function expressions, assigned at execution.


<hr>

Watch Live On Youtube below:

<a href="https://www.youtube.com/watch?v=SHINoHxvTso&ab_channel=AkshaySaini" target="_blank"><img src="https://img.youtube.com/vi/SHINoHxvTso/0.jpg" width="750"
alt="First Class Functions ft. Anonymous Functions in JS Youtube Link"/></a>
