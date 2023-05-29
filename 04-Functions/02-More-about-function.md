# More About Functions

## Lexical Scope

Lexical scope refers to how the availability or accessibility of variables is determined within nested functions or blocks of code. When you declare a variable inside a function or block, it is only accessible within that function or block and any nested functions within it.

Let's consider an example

```js
function outerFunction() {
  const outerVariable = "Hello";

  function innerFunction() {
    console.log(outerVariable); // Hello
  }

  innerFunction();
}

outerFunction();

console.log(outerVariable); // ReferenceError: outerVariable is not defined
```

In this code, we have an `outerFunction` that contains an `innerFunction` nested inside it. Inside the `outerFunction`, there is a variable called `outerVariable` that holds the value `'Hello'`.

Lexical scoping means that the `innerFunction` can access the `outerVariable` because it is declared in the outer scope, which is the `outerFunction`. The inner function "remembers" or retains access to variables declared in its outer scope.

So, when `innerFunction` is executed or called, it can access and use the value of `outerVariable`. In this case, it will log `'Hello'` to the console.

On the other hand, variables declared inside the `outerFunction` are not accessible in any other outer scopes because they are in a more restricted or inner scope. For example, the `outerVariable` is not accessible outside the `outerFunction` because it is declared in the `outerFunction` and not in the global scope i.e why we get a `ReferenceError` when we try to log the value of `outerVariable` outside the `outerFunction`.

Let's see if you can figure out what the following code will log to the console.

```js
const firstName = "Max";

function outerFunction() {
  const firstName = "Ben";

  function innerFunction() {
    const firstName = "Gwen";
    const LastName = "Tennyson";
    console.log(firstName);
    console.log(LastName);
  }

  innerFunction();
}

outerFunction();
console.log(firstName);
console.log(LastName);
```

Before you run the code, try to figure out what the output will be.

Here's what the code will log to the console:

```
Gwen
Tennyson
Max
ReferenceError: LastName is not defined
```

- We start by declaring a global variable `firstName` and assigning it the value `"Max"`. This variable is accessible throughout the entire code.
- Next, we define the function `outerFunction`. Inside `outerFunction`, we declare a new variable `firstName` and assign it the value `"Ben"`. This variable is scoped to the `outerFunction` and does not affect the global `firstName` variable.
- Within `outerFunction`, we define another function called `innerFunction`. Inside `innerFunction`, we declare a new variable `firstName` with the value `"Gwen"`. We also declare a variable `LastName` with the value `"Tennyson"`. Both of these variables are scoped to the `innerFunction` and do not affect the `firstName` variable in the outer scopes.
- When we execute `innerFunction()` inside `outerFunction`, it logs the value of `firstName` within its scope, which is `"Gwen"`, and `LastName`, which is `"Tennyson"`, to the console.
- After executing `innerFunction`, we return to the global scope. Here, we log the value of the global variable `firstName`, which is still `"Max"`, to the console.
- Lastly, we attempt to log the value of `LastName` to the console. However, this will result in an error because `LastName` is not defined in the global scope. It is only accessible within the scope of the `innerFunction`.

**Try to comment out `const firstName = "Gwen";` which is inside the `innerFunction` and see what happens and then comment out `const firstName = "Ben";` which is inside the `outerFunction` and see what happens.**

## Block Scope VS Function Scope

In JavaScript, variables declared with the `var` keyword are scoped to the function in which they are declared. This is called function scope. Variables declared with the `let` and `const` keywords are scoped to the block in which they are declared. This is called block scope.

Want to learn about `var` vs `let and const` click [here](../01-Introduction-to-Javascript/04-Basic-syntax-and-data-types.md)

### **Block Scope:**

Block scope refers to the visibility and accessibility of variables within blocks of code, which are typically defined by curly braces `{}`. Blocks can include `if statements`, `loops`, and any code enclosed within curly braces.

Example of block scope:

```js
if (true) {
  var blockvariable1 = "Hi";
  const blockVariable2 = "Hello";
  console.log(blockVariable1); // "Hi"
  console.log(blockVariable2); // "Hello"
}

console.log(blockVariable1); // "Hi"
console.log(blockVariable2); // ReferenceError: blockVariable is not defined
```

In the example above, we have an `if statement` that contains two variables: `blockVariable1` and `blockVariable2`. Here `blockVariable2` is declared using const which is scoped to the `if statement` block. This means that `blockVariable2` is only accessible within the `if statement` block and not outside of it. While `blockVariable1` is accessible outside the `if statement` block because it is declared using `var` which is scoped to the function in which it is declared.

### **Function Scope:**

Function scope refers to the visibility and accessibility of variables within functions. Variables declared within a function are only accessible within that function or within nested functions inside it.

```js
function myFunction() {
  var functionVariable = "Hi";
  console.log(functionVariable); // "Hi"
}

console.log(functionVariable); // ReferenceError: functionVariable is not defined
```

In this example, `functionVariable` is declared within the function `myFunction`. It is accessible only within that function, and any attempts to access it outside the function will result in a reference error.

## Default Parameters

Default parameters in JavaScript allow you to assign default values to function parameters in case no value or an undefined value is passed when the function is called. This helps provide fallback values and increases the flexibility and robustness of your functions.

Here's an example that demonstrates the usage of default parameters:

```js
function greet(name = "Anonymous") {
  console.log(`Hello, ${name}!`);
}

greet(); // Output: Hello, Anonymous!
greet("John"); // Output: Hello, John!
```

In the example above, the `greet` function has a single parameter called `name`. By using the `=` operator, we assign the default value `"Anonymous"` to the `name` parameter.

When the `greet` function is called without passing any argument, the default parameter value `"Anonymous"` is used. It prints `"Hello, Anonymous!"` to the console.

However, if an argument is provided when calling the function, such as `"John"`, the default parameter value is overridden, and the passed value is used instead. It prints `"Hello, John!"` to the console.

Default parameters can also be expressions or function calls. Here's an example illustrating this:

```js
function calculateArea(length, width = 10) {
  return length * width;
}

console.log(calculateArea(5)); // Output: 50
console.log(calculateArea(5, 8)); // Output: 40
```

Default parameters provide a convenient way to handle missing or undefined values in function arguments and improve the flexibility of your functions.

## Rest Parameters

The rest parameter is a feature in JavaScript that allows a function to accept an indefinite number of arguments as an array. It enables you to pass multiple arguments into a function without explicitly defining them as separate parameters.

The rest parameter is denoted by the ellipsis (...) followed by a parameter name. When the function is called, any remaining arguments that are not assigned to previous parameters are collected into an array using the rest parameter.

Here's an example that demonstrates the usage of the rest parameter:

```js
function sum(...numbers) {
  let total = 0;
  for (let number of numbers) {
    total += number;
  }
  return total;
}

console.log(sum(1, 2, 3, 4, 5)); // Output: 15
console.log(sum(10, 20, 30)); // Output: 60
```

In the example above, the `sum` function uses the rest parameter `...numbers` to accept any number of arguments passed to it. The rest parameter collects all the arguments into an array called `numbers`.

Inside the function, we iterate over the `numbers` array and accumulate the values by adding them to the total variable. Finally, the total sum is returned.

When we call the `sum` function with multiple arguments, such as `1, 2, 3, 4, 5,` the rest parameter collects these values into an array `[1, 2, 3, 4, 5]`. The function then calculates the sum of all the numbers, which is `15`.

Similarly, when we call the function with `10, 20, 30,` the rest parameter collects these values into an array `[10, 20, 30]`, and the sum is calculated as `60`.

The rest parameter provides a concise and flexible way to handle variable-length argument lists within a function. It allows you to work with an arbitrary number of arguments without explicitly defining each one as a separate parameter.

## Parameters Desctructuring

Parameter destructuring is an important feature in JavaScript that allows you to extract values from objects or arrays and assign them to individual variables within function parameters. It provides a concise way to access specific properties or elements of complex data structures passed to a function.

Here's an example that demonstrates parameter destructuring with objects:

```js
function greet({ firstName, lastName, sex: gender, age }) {
  console.log(
    `Hello, my name is ${firstName} ${lastName}.${gender} and ${age} years old.`
  );
}

const person = { firstName: "John", lastName: "Doe", sex: "Male", age: 25 };

greet(person); // Output: Hello, my name is John Doe. Male and 25 years old.
```

## Function Return Function

As we can return any data type from a function, it is also possible to return a function from a function. A function that returns another function is called a higher-order function.

Here's an example that demonstrates this:

```js
function greeting(message) {
  return function (name) {
    console.log(message + ", " + name + "!");
  };
}

const sayHello = greeting("Hello");
console.log(sayhello); // Outputs: ƒ (name) { console.log(message + ", " + name + "!"); }

sayHello("John"); // Output: Hello, John!

const sayHi = greeting("Hi");
sayHi("Jane"); // Output: Hi, Jane!
```

## Callback Functions

A callback function is a function that is passed as an argument to another function and is invoked or executed inside that function. Callback functions are a fundamental concept in JavaScript, particularly for handling asynchronous operations and event-driven programming.

We will learn more about asynchronous operations and event-driven programming in the upcoming sections. For now, let's focus on understanding the basics of callback functions.

```js
function addtwoNum(callback) {
  const result = 2 + 2;

  callback(result); // Execute the callback function
}

function callbackFunction(value) {
  console.log("The result is:", value);
}

addtwoNum(callbackFunction);
```

In this example, the `addtwoNum` takes a callback function as an argument and invokes it immediately, passing the result of the computation (2 + 2) as the argument. The `callbackFunction` is executed synchronously, and the result is logged to the console.

**Anonymous Function as a Callback:**
You can also use an anonymous function as a callback directly within the function call.

```js
function processNumbers(numbers, callback) {
  const poppedvalue = number.pop();

  callback(poppedvalue); // Execute the callback function
}

const numbers = [1, 2, 3, 4, 5];

processNumbers(numbers, function (result) {
  console.log("Popped Value:", result); // Output: Popped Value: 5
}); // numbers and anonymous function are passed as arguments
```

**Higher-Order Functions:**
We already know about Higher-order-function. Let's see how Higher-order functions and callback function works together.

```js
function calculator(num1, num2, operation) {
  return operation(num1, num2);
}

function add(num1, num2) {
  return num1 + num2;
}

function subtract(num1, num2) {
  return num1 - num2;
}

const result1 = calculator(5, 3, add);
console.log("Addition:", result1); // Output: Addition: 8

const result2 = calculator(5, 3, subtract);
console.log("Subtraction:", result2); // Output: Subtraction: 2
```

In this example, the `calculator` function is a higher-order function that takes two numbers and an operation function as arguments. It invokes the operation function, passing the two numbers as arguments, and returns the result.

The add and subtract functions are passed as callbacks to the calculator function, performing addition and subtraction operations, respectively. The results are then logged to the console.
