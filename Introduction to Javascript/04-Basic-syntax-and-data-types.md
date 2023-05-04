# Basic Syntax And Data Types

The JavaScript has a simple syntax and supports a variety of data types.

## **Variables**

Variables are used to store values. A variable is declared using the **_var_**, **_let_**, or **_const_** keyword, followed by a variable name, and an optional initial value. For example:

```
var myName = "John";
let myAge = 25;
myAge = 21; // --> we can change the value of a variable
console.log(myAge); //  21
const PI = 3.14;
```

In the above example,

- `myName` is a variable of type `string` with an initial value of "John",
- `myAge` is a variable of type `number` with an initial value of 25, and then `myAge` changed the value to 21. -
- `PI` is a `constant` of type `number` with a value of 3.14. **_We cannot change the value of a constant._**

**Here are some rules to keep in mind when naming variables in JavaScript:**

- The first character must be a letter, underscore ( \_ ), or dollar sign ( $ ). It cannot be a number or any other character.
- Variable names can only contain letters, numbers, underscores, and dollar signs. No spaces or special characters are allowed.
- Variable names are case sensitive, meaning that "myVar" and "myvar" are considered two different variables.
- Avoid using reserved keywords such as "if", "else", "for", "while", and "function" as variable names.
- Choose descriptive names that reflect the purpose of the variable. This will make it easier to understand the code and modify it in the future.

_Here are some examples of valid variable names:_

```
var name = "John";
var age = 30;
var _count = 10;
var $price = 9.99;
var firstName = "Jane";
```

_And here are some examples of invalid variable names:_

```
var 2ndName = "Smith"; // --> cannot start with a number
var my-var = "test"; // --> cannot contain a hyphen
var function = "hello"; // --> cannot use a reserved keyword as a variable name
```

In JavaScript, there are three different ways to declare variables: **_var_**, **_let_**, and **_const_**. Each has its own unique properties and use cases. Take a look at each one in detail [here](#var-vs-let-and-const).

## **Data Types**

JavaScript supports the following basic data types:

### **Numbers:**

In JavaScript, numbers can be integers or floating-point numbers. For example:

```
var num1 = 10;     // --> integer
var num2 = 3.14;   // --> floating-point number
```

---

### **Strings:**

Strings are used to represent text in JavaScript. A string is enclosed in single or double quotes. For example:

```
var name = "John";   // --> using double quotes
var message = 'Hello, World!';  // --> using single quotes
```

**String indexing** refers to accessing individual characters in a string by their position or index.

```
let str = "hello";
// string --> h e l l o
// index  --> 0 1 2 3 4

console.log(str[4]); // outputs o
```

**Some Imporstant Strings Methods**

**1. trim()** - It returns a new string with the whitespace characters removed from both the beginning and the end and does not modify the original string.

```
let str = "    Hello, World!    ";
let trimmedStr = str.trim();

console.log(trimmedStr); // outputs "Hello, World!"
```

**2. toUpperCase()** - returns a string with all characters converted to uppercase.

```
const str = "hello";
console.log(str.toUpperCase()); // outputs "HELLO"
```

**3. toLowerCase()** - returns a string with all characters converted to lowercase.

```
const str = "HELLO";
console.log(str.toLowerCase()); // outputs "hello"
```

**4. slice()**: returns a portion of a string based on the specified start and end index.

```
const str = "hello world";
console.log(str.slice(0, 5)); // outputs "hello"
```

**5. length**: returns the length of a string.

```
const str = "hello";
console.log(str.length); // outputs 5
```

**6. concat()**: joins two or more strings together.

```
const str1 = "hello";
const str2 = "world";
console.log(str1.concat(" ", str2)); // outputs "hello world"
console.log(str1 + " " + str2); // outputs "hello world"
```

**Template String**
Template strings, also known as `template literals`, are a way to create strings in JavaScript that allow for easier interpolation of variables and expressions. They were introduced in ECMAScript 6 as a new syntax for creating strings.

Template strings are enclosed in backticks (`) instead of single or double quotes. They allow for embedding variables and expressions directly within the string using ${...} syntax. For example:

```
const name = "Alice";
console.log(`Hello, ${name}!`); // outputs Hello, Alice!
```

Template strings can also span multiple lines without the need for escape characters, making them ideal for creating multiline strings or complex string concatenation.

---

### **Booleans:**

A boolean value represents a logical value of either true or false. For example:

```
var isStudent = true;   // true
var isWorking = false;  // false
```

---

### **Undefined:**

The undefined data type represents a variable that has not been assigned a value. For example:

```
let x;
console.log(typeof x); // outputs undefined
```

---

### **Null:**

The null value represents the intentional absence of any object value. For example:

```
let x = null;
console.log(typeof x); // what will be the output?
x = "10"
console.log(typeof x); // what will be the output?
```

---

### **Objects:**

Objects are used to represent complex data structures in JavaScript. An object is a collection of properties, where each property is a key-value pair. For example:

```
let person = {
    name: "John",
    age: 25,
    address: {
        street: "123 Main St",
        city: "New York"
    }
};

console.log(typeof person); // outputs objects

let arr = [1,2,3,4,5];
console.log(typeof arr); // what will be the output?
```

---

## **Comments**

Comments are used to add explanatory notes to the code. In JavaScript, comments can be single-line or multi-line. For example:

```

// This is a single-line comment

/_
This is a
multi-line
comment
_/

```

---

### **Key Concepts :**

**typeof null** returns "object" in JavaScript. This is a known quirk of the language and is due to historical reasons. It's not technically correct to say that null is an object, but it's a common mistake that's made because of the way typeof works in JavaScript.

**Functions and Arrays** are objects in JavaScript.

---

## **var vs let and const**

### **var :**

- Variables declared with var are function-scoped, meaning they can be accessed anywhere within the function they are declared in, including nested functions.
- Variables declared with var can be re-declared and updated within the same scope.
- If a var variable is declared outside of a function, it becomes a global variable and can be accessed anywhere in the code, including other functions and files.

```
function example() {
  var x = 5;
  if (true) {
    var x = 10;
    console.log(x); // outputs 10
  }
  console.log(x); // outputs 10
}

example();
```

### **let :**

- Variables declared with let are block-scoped, meaning they can only be accessed within the block they are declared in, including nested blocks.
- let variables cannot be re-declared within the same block scope, but their value can be updated.
- let variables are commonly used in for-loops to avoid unintended consequences caused by var.

```
function example() {
  let x = 5;
  if (true) {
    let x = 10;
    console.log(x); // outputs 10
  }
  console.log(x); // outputs 5 --> cannot access the variable declared inside the if block
}

example();
```

### **const :**

- const variables cannot be re-declared or updated within the same block scope, meaning their value remains constant throughout the program.
- const is commonly used for values that are not expected to change, such as mathematical constants or configuration settings.
