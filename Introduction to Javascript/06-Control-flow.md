# JavaScript Control Flow

## **Introduction**

Control flow in JavaScript refers to the way statements are executed in a program. It helps us make decisions, repeat code, and handle errors. Understanding control flow is important for writing good JavaScript code. This guide will cover the main control flow structures in JavaScript and provide examples for better understanding.

## **Table of Contents**

- [JavaScript Control Flow](#javascript-control-flow)
  - [**Introduction**](#introduction)
  - [**Table of Contents**](#table-of-contents)
  - [**Conditional Statements**](#conditional-statements)
    - [1. **if statement**](#1-if-statement)
    - [2. **if...else statement**](#2-ifelse-statement)
    - [3. **if...else if ...else statement**](#3-ifelse-if-else-statement)
    - [4. **switch statement**](#4-switch-statement)
  - [**Loops**](#loops)
    - [1. **for loop**](#1-for-loop)
    - [2. **while loop**](#2-while-loop)
    - [3. **do...while loop**](#3-dowhile-loop)
    - [4. **for...in loop**](#4-forin-loop)
    - [5. **for...of loop**](#5-forof-loop)
  - [**Exception Handling**](#exception-handling)
    - [1. **try...catch statement**](#1-trycatch-statement)
    - [2. **finally block**](#2-finally-block)

## **Conditional Statements**

### 1. **if statement**

The `if` statement is used to execute a block of code if a specified condition is true. Here's the syntax for the `if` statement:

```js
if (condition) {
  // code to be executed if the condition is true
}
```

### 2. **if...else statement**

The `if...else` statement allows you to execute different blocks of code based on whether a condition is true or false. Here's the syntax for the `if...else` statement:

```js
if (condition) {
  // code to be executed if the condition is true
} else {
  // code to be executed if the condition is false
}
```

### 3. **if...else if ...else statement**

The `if...else if...else` statement allows you to execute different blocks of code based on different conditions. Here's the syntax for the `if...else if...else` statement:

```js
if (condition1) {
  // code to be executed if condition1 is true
} else if (condition2) {
  // code to be executed if condition2 is true
} else {
  // code to be executed if both condition1 and condition2 are false
}
```

### 4. **switch statement**

The `switch` statement provides a concise way to execute different blocks of code based on the value of an expression.

```js
switch (expression) {
  case value1:
    // code to be executed if expression matches value1
    break;
  case value2:
    // code to be executed if expression matches value2
    break;
  default:
    // code to be executed if expression doesn't match any values
    break;
}
```

---

## **Loops**

### 1. **for loop**

The `for` loop allows you to execute a block of code repeatedly for a specific number of times.
Here is the syntax for the `for` loop:

```js
for (initialization; condition; increment / decrement) {
  // code to be executed in each iteration
}
```

example:

```js
for(int i = 0; i < 5; i++){
    // code to be executed in each iteration
}
```

### 2. **while loop**

The `while loop` repeatedly executes a block of code as long as a specified condition is true.
Here is the syntax for the `while loop`:

```js
while (condition) {
  // code to be executed while the condition is true
}
```

### 3. **do...while loop**

The `do...while loop` is similar to the `while loop`, but it always executes the code block at least once, even if the condition is initially false.
Here is the syntax for the `do...while loop`:

```js
do {
  // code to be executed
} while (condition);
```

example:

```js
let count = 0;

do {
  console.log("Count: " + count);
  count++;
} while (count < 5);

// what will be the output of the above code?
```

In this example, we initialize a variable count to `0`. The `do...while` loop will always execute the code block at least once, regardless of the condition. Inside the loop, we log the value of count to the console and increment it by `1`. The loop continues executing as long as the condition count < `5` is true.

### 4. **for...in loop**

The `for...in` loop is primarily used to iterate over the properties of an object or an array although in array it's generally recommended to use the `for...of` loop instead.

Here is the syntax for the `for...in` loop:

```js
for (variable in object) {
  // code to be executed
}
```

example:

```js
const array = ["apple", "banana", "orange"]; // it means {0: "apple", 1: "banana", 2: "orange"}

for (let index in array) {
  console.log(index + ": " + array[index]);
}

const object = { name: "John", age: 30, occupation: "teacher" };

for (let obj in object) {
  console.log(obj + ": " + object[obj]);
}

// what will be the output?
```

### 5. **for...of loop**

The `for...of` loop allows you to iterate over iterable objects such as arrays, strings, and more.

```js
for (variable of iterable) {
  // code to be executed for each element
}
```

---

## **Exception Handling**

### 1. **try...catch statement**

The `try...catch` statement is used to handle errors or exceptions that may occur in your JavaScript code. It allows you to define a block of code to be tested for errors, and if an error occurs, it provides a way to catch and handle that error.

Here is the syntax for the `try...catch` statement:

```js
try {
  // code that might throw an exception
} catch (error) {
  // code to handle the exception
}
```

Here's an example to illustrate the try...catch statement:

```js
function divide(a, b) {
  try {
    if (b === 0) {
      throw new Error("Divide by zero error");
    }
    const result = a / b;
    console.log("Result: " + result);
  } catch (error) {
    console.log("Error occurred: " + error.message);
  }
}

divide(10, 2); // Result: 5
divide(10, 0); // Error occurred: Divide by zero error
```

In this example, we have a function called `divide` that takes two parameters, `a` and `b`. Inside the try block, we divide `a` by `b` to calculate the `result`. However, before performing the division, we check if `b` is equal to `0`. If it is, we deliberately throw an Error with a custom message using the `throw` keyword.

If an error occurs within the `try` block, the execution immediately jumps to the corresponding `catch` block. The `catch` block receives the error object as a parameter (in this case, named error). Inside the `catch` block, we can handle the error appropriately. In this example, we simply log the error message to the console.

When we call the `divide` function with different arguments, the first call `divide(10, 2)` executes successfully and logs the result. However, the second call `divide(10, 0)` encounters an error due to dividing by zero. The error is caught by the `catch` block, and we log the error message to the console.

### 2. **finally block**

The finally block is optional and is executed regardless of whether an exception is thrown or caught. It is typically used to release resources or perform cleanup tasks.

```js
try {
  // code that might throw an exception
} catch (error) {
  // code to handle the exception
} finally {
  // code to be executed regardless of exceptions
}
```

---
