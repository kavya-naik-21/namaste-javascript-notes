# Episode 5 : Shortest JS Program, window & this keyword

- **The shortest JS program is empty file**. Because even then, JS engine does a lot of things. As always, even in this case, it creates the GEC which has memory space and the execution context.

- JS engine creates something known as '**window**'. It is an object, which is created in the global space. It contains lots of functions and variables. These functions and variables can be accessed from anywhere in the program. JS engine also creates a **this** keyword, which points to the **window object** at the global level. So, in summary, along with GEC, a global object (window) and a this variable are created.

- In different engines, the name of global object changes. Window in browsers, but in nodeJS it is called something else. At global level, this === window

- what is global space -> any code that you write in JS which is not inside a function
    ```js
    var a = 10; // is inside global space
    function b() { // is inside global space
      var x = 10; // is not in gloabal space
    }
    ```
    
- If we create any variable in the global scope, then the variables get attached to the global object.
eg:

```js
var x = 10;
console.log(x); // 10  // from gloabl space // if you don't put anything before it assumes global space
console.log(this.x); // 10 // from gloabl space
console.log(window.x); // 10 // from global space
```

<hr>

Watch Live On Youtube below:

<a href="https://www.youtube.com/watch?v=QCRpVw2KXf8&ab_channel=AkshaySaini" target="_blank"><img src="https://img.youtube.com/vi/QCRpVw2KXf8/0.jpg" width="750"
alt="Shortest JS Program, window & this keyword Youtube Link"/></a>
