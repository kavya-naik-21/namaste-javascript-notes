# Episode 10 : Closures in JS

- Function bundled along with it's lexical scope is **closure**.

- JavaScript has a lexcial scope environment. If a function needs to access a variable, it first goes to its local memory. When it does not find it there, it goes to the memory of its lexical parent. See Below code, Over here function **y** along with its lexical scope i.e. (function x) would be called a closure.

  ```js
  function x() {
    var a = 7;
    function y() {
      console.log(a);
    }
    return y;
  }
  var z = x();
  console.log(z); // value of z is entire code of function y.
  ```

  - In above code, When y is returned, not only is the function returned but the entire closure (fun y + its lexical scope) is returned and put inside z. So when z is used somewhere else in program, it still remembers var a inside x()

- Another Example

```js
function z() {
  var b = 900;
  function x() {
    var a = 7;
    function y() {
      console.log(a, b);
    }
    y();
  }
  x();
}
z(); // 7 900
```

- Thus In simple words, we can say:
  - **\*A closure is a function** that has access to its outer function scope even after the function has returned. Meaning, A closure can remember and access variables and arguments reference of its outer function even after the function has returned.\*

<br>

- ![Closure Explaination](/assets/closure.jpg "Lexical Scope")



```
//Example 1

function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  y();
}

x();
```
```
//Example 2 - Assigning entire function to a variable

function x(){
  var a = function y(){
    console.log(a);
  };
  
  y();
}

x();
```
```
//Example 3 - Passing an entire function as a parameter inside another function

function x(){
  var a = 7;
  
  y();
}

x(function y(){
    console.log(a);
  });
```
```
//Example 4 - return a function from a function

function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  return y;
}

x();
```
```
//Example 5 - extension of Example 4

function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  return y;
}

//console.log(z);
var z = x();
console.log(z);
```
-----------------------
When functions are returned from another fun, they still maintain their lexical
scope.
 ```
 //Example 6
 
function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  return y; //line 6
}

var z = x(); //line 9
console.log(z);
//....................after 1000 lines of code
z(); //line XXD
```
- When y is returned, not only is the function returned but the entire closure (func. y + its lexical scope) is returned and put inside z. Basically at line 5 not just y function was returned but at line 5 the y function along with the lexical scope of y function was returned. Therefore as lexical scope is returned that is why when z is used somewhere else in program like line XXD, it still remembers var a inside x() //so even though after line 9 evn though x() function or x EC no longer exists in the memory but the y() function still remembers its lexical scope/environment or basically where it came from 
- So even though the x function is lost or no longer accessible after line 9, the y function still has a strong binding with its parent x function. This is because the y function is a closure. A closure is a function that has access to the variables of its enclosing scope, even after the enclosing scope has been closed.
- Closure is a very powerful concept of JS, just because this function remembers things even if they are not in their lexical scope

 ```
 //Example 7 - same just another way of writing Example 6
 
function x(){
  var a = 7;
  return function y(){
    console.log(a);
  }
}

var z = x(); 
console.log(z);
//....................after 1000 lines of code
z(); //line XXD
```
### Corner Cases (JS Closure GOTCHAs)
```
//Example 8

function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  a = 100;
  return y;
}
//console.log(z);
var z = x();
console.log(z);
z(); // output will be 100 -- because function along with it's reference to the variable is returned
// the reference points to 100, and 100 is still in memory preserved
// when x was gone it was not garbage collected, because it has to be used later
// in this way closure gives us 100
```
```
//Example 9

function z() {
  var b = 900; 
  function x(){
    var a = 7;
    function y(){
      //var a = 22;
      console.log(a,b);
      //var a = 22;
    }
    y();
  }
  x();
}
z();
```
for above code-> y has a closure of x along with closure of z, parents parents parents ......... inf

![image](https://github.com/user-attachments/assets/6a35a6f9-2ca3-4f92-954a-8d2fddfc3580)


* Advantages of Closure:

      Certainly! Let's explore examples for each of the advantages you've
      mentioned:

  1.  **Module Design Pattern**:

      - The module design pattern allows us to encapsulate related
        functionality into a single module or file. It helps organize
        code, prevent global namespace pollution, and promotes
        reusability.
      - Example: Suppose we're building a web application, and we want
        to create a module for handling user authentication. We can
        create a `auth.js` module that exports functions like `login`,
        `logout`, and `getUserInfo`.

        ```js
        // auth.js
        const authModule = (function () {
          let loggedInUser = null;

          function login(username, password) {
            // Authenticate user logic...
            loggedInUser = username;
          }

          function logout() {
            loggedInUser = null;
          }

          function getUserInfo() {
            return loggedInUser;
          }

          return {
            login,
            logout,
            getUserInfo,
          };
        })();

        // Usage
        authModule.login("john_doe", "secret");
        console.log(authModule.getUserInfo()); // 'john_doe'
        ```

  2.  **Currying**:

      - Currying is a technique where a function that takes multiple
        arguments is transformed into a series of functions that take
        one argument each. It enables partial function application and
        enhances code flexibility.
      - Example: Let's create a curried function to calculate the total
        price of items with tax.

        ```js
        const calculateTotalPrice = (taxRate) => (price) =>
          price + price * (taxRate / 100);

        const calculateSalesTax = calculateTotalPrice(8); // 8% sales tax
        const totalPrice = calculateSalesTax(100); // Price with tax
        console.log(totalPrice); // 108
        ```

  3.  **Memoization**:

      - Memoization optimizes expensive function calls by caching their
        results. It's useful for recursive or repetitive computations.
      - Example: Implement a memoized Fibonacci function.

        ```js
        function fibonacci(n, memo = {}) {
          if (n in memo) return memo[n];
          if (n <= 1) return n;

          memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
          return memo[n];
        }

        console.log(fibonacci(10)); // 55
        ```

  4.  **Data Hiding and Encapsulation**:

      - Encapsulation hides the internal details of an object and
        exposes only necessary methods and properties. It improves code
        maintainability and security.
      - Example: Create a `Person` class with private properties.

        ```js
        class Person {
          #name; // Private field

          constructor(name) {
            this.#name = name;
          }

          getName() {
            return this.#name;
          }
        }

        const person = new Person("Alice");
        console.log(person.getName()); // 'Alice'
        // console.log(person.#name); // Error: Private field '#name' must be declared in an enclosing class
        ```

  5.  **setTimeouts**:

      - `setTimeout` allows scheduling a function to run after a
        specified delay. It's commonly used for asynchronous tasks,
        animations, and event handling.
      - Example: Delayed message display.

        ```js
        function showMessage(message, delay) {
          setTimeout(() => {
            console.log(message);
          }, delay);
        }

        showMessage("Hello, world!", 2000); // Display after 2 seconds
        ```

  These examples demonstrate the power and versatility of closures in
  JavaScript! 🚀

- Disadvantages of Closure:
  - Over consumption of memory
  - Memory Leak
  - Freeze browser

<hr>

Watch Live On Youtube below:

<a href="https://www.youtube.com/watch?v=qikxEIxsXco&ab_channel=AkshaySaini" target="_blank"><img src="https://img.youtube.com/vi/qikxEIxsXco/0.jpg" width="750"
alt="Closure in JS Youtube Link"/></a>
