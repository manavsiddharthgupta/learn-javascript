# Basic Operators

Operators in JavaScript are symbols or keywords used to perform operations on values or variables. In this section, we will cover some of the basic operators in JavaScript.

## **Arithmetic Operators**

Arithmetic operators are used to perform arithmetic operations on numbers (literals or variables). The following table lists the arithmetic operators in JavaScript:

- `+` Addition - adds two numbers together
- `-` Subtraction - subtracts one number from another
- `*` Multiplication - multiplies two numbers together
- `/` Division - divides one number by another
- `%` Modulus - gives the remainder of one number divided by another

```js
let a = 5;
let b = 2;
let c = a + b; // --> c now contains the value 7
let d = a - b; // --> c now contains the value 3
let e = a * b; // --> c now contains the value 10
let f = a / b; // --> c now contains the value 2.5
let g = a % b; // --> c now contains the value 1
```

## **Assignment Operators**

Assignment operators are used to assign values to variables. They're like a shortcut for writing variable = variable + value. Here are some examples of assignment operators in JavaScript:

- `=` Assigns the value on the right to the variable on the left.
- `+=` Adds the value on the right to the variable on the left, and assigns the result to the variable on the left.
- `-=` Subtracts the value on the right from the variable on the left, and assigns the result to the variable on the left.
- `*=` Multiplies the variable on the left by the value on the right, and assigns the result to the variable on the left.
- `/=` Divides the variable on the left by the value on the right, and assigns the result to the variable on the left.
- `%=` Calculates the modulo of the variable on the left and the value on the right, and assigns the result to the variable on the left.

```js
let a = 5;
let b = a; // --> b now contains the value 5
a += 2; // --> a now contains the value 7
a -= 2; // --> a now contains the value 5
a *= 2; // --> a now contains the value 10
a /= 2; // --> a now contains the value 5
a %= 2; // --> a now contains the value 1
```

## **Comparison Operators**

Comparison operators are like a referee in a wrestling match. They compare two values and declare a winner (or loser). Here are some examples of comparison operators in JavaScript:

- `==` Equal to - compares two values to see if they're equal, but they don't care about the data type.
- `===` Strict equal to - compares two values to see if they're equal, but they also check the data type.
- `!=` Not equal to - compares two values to see if they're not equal, they don't care about the data type.
- `!==` Strict not equal to - compares two values to see if they're not equal, and also checks the data type.
- `>` Greater than
- `<` Less than
- `>=` Greater than or equal to
- `<=` Less than or equal to

```js
let a = 5;
let b = "5";
let c = 2;
console.log(a == b); //  --> true - because they look the same
console.log(a === b); //  --> false - because they're not the same type
console.log(a != b); //  --> false - because string will converted into number and here both are same
console.log(a !== b); //  --> true - because they're not the same type
console.log(a > c); //  --> true - because 5 is greater than 2
console.log(a < c); //  --> false - because 5 is not less than 2
console.log(a >= c); //  --> true - because 5 is greater than or equal to 2
console.log(a <= c); //  --> false - because 5 is not less than or equal to 2
```

## **Logical Operators**

- `&&` Logical AND - checks if both conditions are true, and returns true only if both are true.

  ```js
  let a = 5;
  let b = 10;
  let c = 15;
  console.log(a < b && b < c); //  --> true - because both conditions are true
  console.log(a < b && b > c); //  --> false - because one of the conditions is false
  ```

- `||` Logical OR - checks if at least one condition is true, and returns true if at least one is true.

  ```js
  let a = 5;
  let b = 10;
  let c = 15;
  console.log(a < b || b > c); //  --> true - because at least one condition is true
  console.log(a > b || b > c); //  --> false - because both conditions are false
  ```

- `!` Logical NOT - flips the value of a condition. If it's true, it returns false. If it's false, it returns true.

  ```js
  let a = 5;
  let b = 10;
  let c = 15;
  console.log(!(a < b)); //  --> false - because a < b is true
  console.log(!(a > b)); //  --> true - because a > b is false
  ```
