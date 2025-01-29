# Episode 2 : How JS is executed & Call Stack

- When a JS program is ran, a **global execution context** is created.

- The execution context is created in two phases.

  - Memory creation phase - JS will allocate memory to variables and functions.
  - Code execution phase

- Let's consider the below example and its code execution steps:

```js
var n = 2;
function square(num) {
  var ans = num * num;
  return ans;
}
var square2 = square(n);
var square4 = square(4);
```
When we execute the above code, execution context is created, 
Execution context is created in 2 phases

The very **first** thing which JS does is **memory creation phase**, so it goes to line 1 of above code snippet, and **allocates a memory space** for variable **'n'** and then goes to line two, and **allocates a memory space** for **function 'square'**. When allocating memory **for n it stores 'undefined'**, a special value for 'n'. **For 'square', it stores the whole code of the function inside its memory space.** Then, as square2 and square4 are variables as well, it allocates memory and stores 'undefined' for them, and this is the end of first phase i.e. memory creation phase.

So O/P will look something like

![Execution Context Phase 1](/assets/phase1.jpg "Execution Context")

Now, in **2nd phase** i.e. **code execution phase**, it starts going through the whole code line by line. This is the point where functions and every calculation in the program is done.

As it encounters var n = 2, it assigns 2 to 'n'. Until now, the value of 'n' was undefined. 
In line 2, i.e., For function,  there is nothing to execute. As these lines were already dealt with in memory creation phase.

Coming to line 6 i.e. **var square2 = square(n)**, here function invocation is happening, here **functions are a bit different than any other language, when a function is invoked - A new execution context is created altogether.** Again in this new execution context, in memory creation phase, we allocate memory to num(i.e., **parameters**) and ans the two variables. And undefined is placed in them. Now, in code execution phase of this execution context, first 2 is assigned to num. num \* num will happen in code phase. Then var ans = num \* num will store 4 in ans. After that, return ans returns the control of program back to execution context where this function was invoked from.

![Execution Context Phase 2](/assets/phase2.jpg "Execution Context")

When **return** keyword is encountered, It returns the control to the called line and also **the function execution context is deleted**.
Same thing will be repeated for square4 and then after that is finished, the global execution context will be destroyed.
So the **final diagram** before deletion would look something like:

![Execution Context Phase 2](/assets/final_execution_context.jpg "Execution Context")

- Javascript manages code execution context creation and deletion with the the help of **Call Stack**. JS has it's own callstack

- Call Stack is a mechanism to keep track of its place in script that calls multiple function.
- Call Stack is like a stack, in the bottom of the stack we have our global execution context,
 ![image](https://github.com/user-attachments/assets/d8fc3ea3-f678-4161-8dc3-6de021f58a29)

![image](https://github.com/user-attachments/assets/1431ad96-f21e-4cfa-b34c-aea523ef9f4e)

  -- That means, whenever any JS program is run, this call stack is populated with this Global execution context. This whole execution context is pushed inside this stack
  -- Whenever a function is invoked, or a new execution context is created, So this execution context is put inside the stack. example E1, which is the execution context 1, Once we are done with executing this function, we return the ans, E1 is moved out. E1 is popped out of the stack, and the control goes back to the global execution context, where it left.
  -- similarly with E2 as well and the control goes back to Global Execution Context (GEC).
  --  this call stack is only for managing these Execution contexts.
  --  whenever an Execution context is deleted, it will move out of the stack.
  -- After this whole thing is executed, the call stack gets empty.
- Core Concept - Call Stack maintains the order of execution of execution contexts. It is also known as Program Stack or Control Stack or Runtime stack or Machine Stack or Execution context stack.

<hr>

Watch Live On Youtube below:

<a href="https://www.youtube.com/watch?v=iLWTnMzWtj4&t=1s&ab_channel=AkshaySaini" target="_blank"><img src="https://img.youtube.com/vi/iLWTnMzWtj4/0.jpg" width="750"
alt="How JS is executed & Call Stack Youtube Link"/></a>
