# Introduction to Functions

## What is a Function?

In JavaScript, functions are like building blocks that you can use to group a bunch of instructions and make them work together to do something specific. They are really handy because they let you reuse your code, keep things organized, and do different tasks in separate parts.

A function in JavaScript is defined using the `function` keyword, followed by a name (also known as the function identifier), a set of parentheses `()`, and a pair of curly braces `{}` that enclose the function's body. The body contains the code that will be executed when the function is called.

```js
function functionName() {
  // Function body
  // Code to be executed
}
```

### **Function Invocation**

Now that you have created a function, you can execute the code inside it by calling it from anywhere in your code. To call a function, you simply write its name followed by a pair of parentheses `()`.

```js
functionName(); // Function call
```

Function invocation triggers the execution of the function's code from the top to the bottom. You can call a function multiple times from different parts of your program.

### **Function Parameters and Arguments**

Functions in JavaScript can accept input values known as parameters. Parameters are defined inside the parentheses when declaring the function, separated by commas if there are multiple parameters. They act as placeholders for values that will be passed to the function when it is called.

```js
function greet(name) {
  console.log("Hello" + name + "!");
}
```

In the example above, `name` is a parameter of the `greet` function.

When calling a function, you can provide specific values, known as arguments, to be assigned to the corresponding parameters.

```js
greet("Ben");
```

In this case, the string "Ben" is an argument passed to the greet function, which will assign it to the name parameter.

### **Return Statement**

A function can also return a value back to the caller using the `return` statement. This allows you to obtain the result of a computation or process performed within the function.

```js
function add(a, b) {
  return a + b;
}
```

In the example above, the `add` function takes two parameters `a` and `b`, and it returns the sum of the two values.

To capture the returned value, you can assign it to a variable or use it directly.

```js
let result = add(2, 3);
console.log(result); // 5
```

### **Function Expression**

What we have learn till now is Function Declaration.

In additional to Function Declaration, JavaScript also supports function expressions. A function expression is a function that is assigned to a variable or a constant.

```js
const multiply = function (a, b) {
  return a * b;
};
```

In this example, the `multiply` variable is assigned a function expression. It can be invoked and used just like any other function.

### **Arrow Function**

ES6 (ECMAScript 2015) introduced arrow functions, which provide a more concise syntax for defining functions. They are particularly useful for writing shorter, one-line functions.

```js
const square = (x) => x * x;

const addtwonum = (num1, num2) => {
  return num1 + num2;
};
```

The arrow function `square` takes a parameter `x` and returns its square.
The arrow function `addtwonum` takes two parameter `num1` and `num2` and returns after adding both number.

Arrow functions have a more implicit syntax and do not create their own this value, making them convenient for certain programming scenarios. You will use Arrow function more that Function Expression.

## Conclusion

Functions are a fundamental part of JavaScript. They are used to group a set of instructions and make them work together to do something specific. They are also useful for reusing code, keeping things organized, and doing different tasks in separate parts.

### **Note**

```js
greet(); // what will happen?

function greet() {
  console.log("Hi, how are you");
}
```

when you can call a function before its actual declaration in the code, and JavaScript will still execute the function without throwing an error. **This behaviour specific to function declarations and does not apply to function expressions and arrow functions.**

**_Function declarations are hoisted._**

During the compilation phase, JavaScript scans the code and hoists function declarations to the top, allowing them to be called from anywhere within the same scope, even before their actual declaration in the code.

It's worth noting that this behavior applies only to function declarations, not to function expressions or arrow functions. Those must be defined before they are called, as they are not hoisted.

It's ok if you didn't understand right now. Hoisting is an advance topic. We have covered in Advance Javascript. If you want to learn more about Hoisting. Click [Here]()
