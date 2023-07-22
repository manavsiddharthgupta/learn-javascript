# How JavaScript Works

The JavaScript Engine parses, compiles, and executes the JavaScript code.
Learn more about **[How the JavaScript works](../01-Introduction-to-Javascript//03-How-javascript-works.md)**.

We Know that JavaScript has two phases:

1. Compilation Phase
   - Early Errors Checking
   - Determine the scope of variables
2. Code Execution Phase
   - Create Global Execution Context

We already discussed the **[Compilation Phase](../01-Introduction-to-Javascript//03-How-javascript-works.md)** in the previous section. Now we will discuss the **Code Execution Phase**.

## Global Execution Context

In JavaScript, the Global Execution Context is the environment where your code begins to run. When you open a web page or run a JavaScript file, the JavaScript engine creates this Global Execution Context.

The Global Execution Context has three phases:

1. Execution Context - An execution context is like a container where the code is evaluated and executed. It consists of two main components:
   - Global Object: The Global Object is a special object that provides a foundation for various things in the code. In web browsers, the Global Object is usually the `window` object. When you declare a variable or a function in the global scope (outside any other function), they become properties and methods of this Global Object.
   - `this` Keyword: The `this` keyword refers to the current context, which depends on how a function is called. It may seem a bit advanced for now, but just remember that it's related to how functions work with objects.

---

2. Creation Phase - An execution context is like a container where the code is evaluated and executed. It consists of two main components:
   - Variable Environment: Variables are initialized with undefined, and functions are entirely stored in memory. `this` value is determined here.
   - Scope Chain - The scope chain is created here. It is used to resolve variables and functions.

---

3. Execution Phase - In this phase, the JavaScript engine executes your code line by line. It assigns values to variables and executes functions.
   Javascript is a synchronous, single-threaded language. This means that it executes code line by line. It can only execute one line of code at a time. It has only one call stack, which is used to execute the code. However, it can delegate some tasks to the browser APIs, which are asynchronous. we will discuss this later.

---

Let's take a look at the following example:

```js
console.log(this);
console.log(window);
console.log(firstname);
var firstname = "John";
console.log(firstname);
```

Lets create a Global Execution Context for the above code:

```
             Code Execution                  Global Execution Context
|----------------------------------------|------------------------------|
| 1. console.log(this);                  | window : {...}               |
| 2. console.log(window);                | this : window                |
| 3. console.log(firstname);             | firstname : undefined        |
| 4. var firstname = "John";             |                              |
| 5. console.log(firstname);             |                              |
|----------------------------------------|------------------------------|
```

In the above example, we have five lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …} (output)
Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …} (output)
undefined (output)
firstname : "John"(assigned value)
John (output)
```

Let's take another example:

```js
console.log(this);
console.log(window);
console.log(myFunction);
console.log(fullname);
function myFunction() {
  console.log("Hello World");
}
var firstname = "John";
var lastname = "Doe";
var fullname = firstname + " " + lastname;
console.log(fullname);
```

```
             Code Execution                  Global Execution Context
|----------------------------------------|------------------------------|
| 1. console.log(this);                  | window : {...}               |
| 2. console.log(window);                | this : window                |
| 3. console.log(myFunction);            | myFunction : myFunction(){..}|
| 4. console.log(fullname);              | firstname : undefined        |
| 5. function myFunction(){...}          | lastname : undefined         |
| 6. var firstname = "John";             | fullname : undefined         |
| 7. var lastname = "Doe";               |                              |
| 8. var fullname = firstname + lastname |                              |
| 9. console.log(fullname);              |                              |
|----------------------------------------|------------------------------|
```

In the above example, we have nine lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …} (output)
Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …} (output)
myFunction(){...} (output)
undefined (output)
firstname : "John"(assigned value)
lastname : "Doe"(assigned value)
fullname : "John Doe"(assigned value)
John Doe (output)
```

## Hoisting

Hoisting is a behavior in JavaScript where variable and function declarations are moved to the top of their containing scope during the compilation phase, even before the code is executed.

In previous examples, we have seen that in `line 3`, we are trying to console.log the `myFunction` function, which is declared in line 5. But still, we are able to access the function. This is because of hoisting. Even `firstname`, `lastname` and `fullname` variables are also hoisted because they are declared using the `var` keyword.

This is beacuse of the **Creation Phase** of the Global Execution Context. In the Creation Phase, the JavaScript engine creates the Variable Environment and Scope Chain. In the Variable Environment, it initializes the variables with `undefined` and stores the functions in memory. This is called **Hoisting**.

Note : Only Function Declarations gets stored in memory. Function Expression cannot get stored beacuse they use `var` keyword to declare the function.

Now, let's take a look at the following example:

```js
console.log(myfunction);

var myfunction = function () {
  console.log("Hello World");
};
```

Lets create a Global Execution Context for the above code:

```
             Code Execution                  Global Execution Context
|----------------------------------------|------------------------------|
| 1. console.log(myfunction);            | window : {...}               |
| 2. var myfunction = function(){...}    | this : window                |
| 3. console.log(myfunction);            | myfunction : undefined       |
|----------------------------------------|------------------------------|
```

In the above example, we have two lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
undefined (output)
myfunction : (){...} (assigned value)
function(){...} (output)
```

Why we are getting `undefined` as output in line 1? Because in the Creation Phase, the JavaScript engine initializes the `myfunction` variable with `undefined`. So, when we try to access the `myfunction` variable, it returns `undefined`.

Let's see what happen if we use let or const keyword instead of var keyword:

```js
console.log(myfunction);
console.log(firstName);

const myfunction = function () {
  console.log("Hello World");
};
let firstName = "John";
```

Lets create a Global Execution Context for the above code:

```
             Code Execution                  Global Execution Context
|----------------------------------------|------------------------------|
| 1. console.log(myfunction);            | window : {...}               |
| 2. console.log(firstName);             | this : window                |
| 3. const myfunction = function(){...}  | myfunction : uninitialized   |
| 4. let firstName = "John";             | firstName : uninitialized    |
|----------------------------------------|------------------------------|
```

In the above example, we have four lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Uncaught ReferenceError: Cannot access 'myfunction' before initialization (output)
Uncaught ReferenceError: Cannot access 'firstName' before initialization (output)
firstName : "John"(assigned value)
```

Why we are getting `Uncaught ReferenceError: Cannot access 'myfunction' before initialization` as output? Because in the Creation Phase, the JavaScript engine adds the `myfunction` and `firstName` variable to the Global Environment Record, but it does not initialize it. So, when we try to access the `myfunction` variable, it returns `Uncaught ReferenceError: Cannot access 'myfunction' before initialization`.

Hence, we can say that `let` and `const` variables are hoisted but not initialized.

### Temporal Dead Zone

The Temporal Dead Zone is a behavior in JavaScript where variables declared using `let` and `const` keywords are not accessible before they are initialized. This is because of the **Creation Phase** of the Global Execution Context. In the Creation Phase, the JavaScript engine adds the `myfunction` and `firstName` variable to the Global Environment Record, but it does not initialize it. So, when we try to access the `myfunction` variable, it returns `Uncaught ReferenceError: Cannot access 'myfunction' before initialization`.

## Function Execution Context

When a function is called, the JavaScript engine creates a new execution context for that function. This execution context is called the Function Execution Context. It is similar to the Global Execution Context, but it has some differences.

Let's take a look at the following example:

```js
let foo = "foo";
console.log(foo);
function getFullName(firstName, lastName) {
  console.log(arguments);
  var myVar = "myVar";
  console.log(myVar);
  return firstName + " " + lastName;
}
const fullName = getFullName("John", "Doe");
console.log(fullName);
```

Let's create a Global Execution Context for the above code:

```
             Code Execution                  Global Execution Context
|----------------------------------------|------------------------------|
| 1. let foo = "foo";                    | window : {...}               |
| 2. console.log(foo);                   | this : window                |
| 3. function getFullName(){...}         | foo : uninitialized          |
| 4. const fullName = getFullName("John" | getFullName : function(){...}|
|    , "Doe");                           | fullName : uninitialized     |
| 5. console.log(fullName);              |                              |
|----------------------------------------|------------------------------|
```

In the above example, we have five lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Line 1 : foo : "foo" (assigned value)
Line 2 : foo (output)
Line 3 : already gets stored in memory
Line 4 : Executes the function, this will create a new Function Execution Context. fullName : "John Doe" (assigned value)
Line 5 : John Doe (output)
```

Lets create a Function Execution Context for the above code:

```
             Code Execution                  Function Execution Context
|----------------------------------------|-----------------------------------|
| 1. console.log(arguments);             | arguments : {0: "John", 1: "Doe"} |
| 2. var myVar = "myVar";                | firstName : "John"                |
| 3. console.log(myVar);                 | lastName : "Doe"                  |
| 4. return firstName + " " + lastName;  | myVar : undefined                 |
|                                        |                                   |
|----------------------------------------|-----------------------------------|
```

In the above example, we have four lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Line 1 : arguments : {0: "John", 1: "Doe"} (output)
Line 2 : myVar : "myVar" (assigned value)
Line 3 : myVar (output)
Line 4 : will return "John Doe"
```

## Scope Chain

The Scope Chain is a list of variables and functions that are accessible to a function. It is created during the Creation Phase of the Function Execution Context. It is used to resolve variables and functions.

Let's take a look at the following example:

```js
let lastName = "Doe";
function getFullName(firstName) {
  let fullName = firstName + " " + lastName;
  return fullName;
}
const fullName = getFullName("John");
console.log(fullName);
```

Let's create a Global Execution Context for the above code:

```
             Code Execution                  Global Execution Context
|----------------------------------------|------------------------------|
| 1. let lastName = "Doe";               | window : {...}               |
| 2. function getFullName(){...}         | this : window                |
| 3. const fullName = getFullName("John" | lastName : uninitialized     |
|    , "Doe");                           | getFullName : function(){...}|
| 4. console.log(fullName);              | fullName : uninitialized     |
|----------------------------------------|------------------------------|
```

In the above example, we have four lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Line 1 : lastName : "Doe" (assigned value)
Line 2 : already gets stored in memory
Line 3 : Executes the function, this will create a new Function Execution Context. fullName : "John Doe" (assigned value)
Line 4 : John Doe (output)
```

Lets create a Function Execution Context for the above code:

```
             Code Execution                  Function Execution Context
|----------------------------------------|-----------------------------------|
| 1. let fullName = firstName + " " +    | arguments : {0: "John"}           |
|    lastName;                           | fullName : undefined              |
| 2. return fullName;                    |                                   |
|                                        |                                   |
|----------------------------------------|-----------------------------------|
```

In the above example, we have two lines of code. The JavaScript engine will execute the code line by line. Let's see what happens in each line of code:

```
Line 1 : fullName : "John Doe" (assigned value). Since lastName is not defined in the function, it will look for the variable in the outer environment. It will find the lastName variable in the Global Environment.
Line 2 : will return "John Doe"
```
