# Intro to closures

We already know that functions are first class citizens in JavaScript. This means that we can pass functions around like variables. This also means that functions can return functions from other functions. Learn more about [function returning function](../04-Functions/02-More-about-function.md#function-return-function).

```js
function outer() {
  return function inner() {
    console.log("I am inner function");
  };
}

const innerFn = outer(); // store the returned function in a variable
console.log(innerFn); // [Function: inner]
innerFn(); // I am inner function
```

In the above example, we have a function `outer` which returns another function `inner`. We store the returned function in a variable `innerFn`. We can call the returned function by calling `innerFn()`.

Let's take another example:

```js
function printName(firstName, lastName) {
  return function () {
    console.log(`${firstName} ${lastName}`);
  };
}

const printFullName = printName("John", "Doe");
printFullName(); // John Doe
```

Now, you must be wondering this is expected behaviour. Is it?

Let's analyse the above code by creating `code execution phase` from above code.

```
           code execution phase                         memory creation phase
|------------------------------------------------|-----------------------------------|
| 1. function printName(...) {...}               |     window: {...}                 |
| 2. const printFullName = printName("John",...) |     this: window                  |
| 3. printFullName();                            |     function printName(...) {...} |
|                                                |     printFullName: uninitialized  |
|------------------------------------------------|-----------------------------------|
```

In the above example we have three statements:

1. We have a function `printName` which takes two parameters `firstName` and `lastName` and returns a function which prints the full name.
2. We call the function `printName` with two arguments `John` and `Doe` and store the returned function in a variable `printFullName`.
3. We call the function `printFullName`.  
   **Note:** We are not passing any arguments to the function `printFullName`. But still it prints the full name. How?

Let's execute the above code line by line.

```
Line 1 - function is already defined in memory
Line 2 - printFullName : function() {...} (assigned) // function is called and returned function is stored in variable printFullName. Here Function printName execution context is created and pushed to the call stack.
Line 3 - John Doe (printed) // function is called and executed. Here Function execution context is created and pushed to the call stack.
```

Now Let's create Function execution context for `printName` and `printFullName` function.

Let's create Function execution context for `printName` function first. Here `printName` function will get pushed to the call stack.

```
           code execution phase                local memory creation phase
|--------------------------------------|----------------------------------------------|
| 1. return function () {...}          | arguments: [firstName:"John", lastName:"Doe"]|
|                                      | firstName: "John"                            |
|                                      | lastName: "Doe"                              |
|                                      | function: {...}                              |
|--------------------------------------|----------------------------------------------|
```

In the above example, we have one statement:

1. we have a function which prints the full name is going to be returned.

Now, Let's execute the above code line by line.

```
Line 1 - Nothing happens // function is already defined in memory which is going to be returned.
```

Here `printName` function will get popped from the call stack and `printFullName` function will get pushed to the call stack.

Now, Let's create Function execution context for returned function i.e. `printFullName`.

```
           code execution phase                local memory creation phase
|--------------------------------------|----------------------------------------------|
| 1. console.log(...)                  | arguments: [] -- we are not passing any args |
|--------------------------------------|----------------------------------------------|
```

In the above example, we have one statement:

1. `console.log(`${firstName} ${lastName}`);` Here `firstName` and `lastName` are not defined in the local memory of `printFullName` function. So, it will look for the variables in the Global memory but it will not find the variables there as well. So how it is printing the full name? Something is missing here.

Well, we have a concept called `closure` which is responsible for this behaviour. Let's understand what is closure.

When a function is returned from another function, the returned function will have access to the variables defined in the outer function even after the outer function has returned. This is called `closure`.

Here `printFullName` function has access to the variables `firstName` and `lastName` defined in the outer function `printName` even after the outer function `printName` has returned and popped from the call stack.

See `printName` function local memory again. you will find `firstName` and `lastName` variables there.

When the function

```js
function () {
console.log(`${firstName} ${lastName}`);
};
```

is returned from the function `printName`, it will also carry the reference of the variables `firstName` and `lastName` defined in the outer function `printName`. This is called `closure`.

Now, Let's execute the above code line by line.

```
Line 1 - John Doe (printed)
```

Now, `printFullName` function will get popped from the call stack. and Global execution context will also get popped from the call stack.
