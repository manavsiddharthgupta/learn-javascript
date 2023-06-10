# Primitive VS Reference DataTypes

In programming, `primitive` and `reference` are terms used to describe different types of data and how they are stored and handled in memory. Understanding the distinction between these two concepts is essential for effective programming and memory management.

## **Primitive Data Types**

- The common primitive types include numbers (integer, float), booleans, characters, and symbols.
- When you assign a primitive value to a variable, the variable directly holds that value.

Let's look at an example:

```js
let num1 = 5; // num1 holds the value 5
let num2 = num1; // num2 receives the value of num1 (a copy)
num1 = 10; // Changing num1 does not affect the value of num2
console.log(num1); // Output: 10
console.log(num2); // Output: 5 (num2 is still 5)
```

<div align="center">
 <img src="./images/primitive_arr.png"  width="700" height="400">
</div>

## **Reference Data Types**

- Reference types represent complex objects and are stored as references to memory locations where the actual data is stored.
- Reference types are arrays, objects, and functions.
- When you assign a reference type to a variable, the variable holds a reference (memory address) to the actual data.
- Operations on reference types usually affect the referenced data, as multiple variables can point to the same object.

Let's look at an example:

```js
let arr1 = [1, 2, 3]; // arr1 holds a reference to an array object
let arr2 = arr1; // arr2 receives the same reference as arr1
arr1.push(4); // Modifying arr1 also affects the referenced array
console.log(arr1); // Output: [1, 2, 3, 4]
console.log(arr2); // Output: [1, 2, 3, 4] (arr2 is also affected)
```

<div align="center">
 <img src="./images/reference_arr.png"  width="700" height="400">
</div>

---

### **How to Clone Array**

Before moving forword let me ask you a question can we clone array by assigning it to another variable?

Here are a few common methods to clone an array:

**1. Using the spread operator (...)**

```js
let originalArray = [1, 2, 3];
let clonedArray = [...originalArray];
```

**2. Using the slice() method**

```js
let originalArray = [1, 2, 3];
let clonedArray = originalArray.slice(0);
```

**3. Using the concat() method**

```js
let originalArray = [1, 2, 3];
let clonedArray = [].concat(originalArray); // [] is an empty array
```

### **Shallow vs Deep Copying**

All of these methods create a new array that is a clone of the original array. It's important to note that these methods create a shallow copy, meaning that if the original array contains reference types (objects or arrays), the cloned array will still reference the same objects. If you need a deep copy (cloning the contents of nested objects as well), additional steps are required.

```js
let originalArray = [
  [1, 2],
  [3, 4],
];
let clonedArray = [...originalArray]; // Shallow copy using spread operator

clonedArray[0][0] = 10; // Modifying an element in the nested array of clonedArray

console.log(originalArray); // Output: [[10, 2], [3, 4]]
console.log(clonedArray); // Output: [[10, 2], [3, 4]]
```

In this example, `originalArray` is an array that contains nested arrays. When we perform a shallow copy using the spread operator, `clonedArray` is created with references to the same nested arrays as `originalArray`.

When we modify the element at `index [0][0]` in the nested array of `clonedArray` `(clonedArray[0][0] = 10)`, it also modifies the corresponding element in `originalArray`. This happens because both arrays share references to the same nested arrays.

As a result, both `originalArray` and `clonedArray` are updated with the modified value, and the output shows `[[10, 2], [3, 4]]` for both arrays.

This demonstrates that a shallow copy creates a new array with references to the same nested arrays. Modifying elements within those nested arrays will affect both the original and cloned arrays. To achieve a deep copy where nested arrays are also cloned, additional steps are required.

To create a deep copy using the JSON methods:

```js
let originalArray = [
  [1, 2],
  [3, 4],
];
let clonedArray = JSON.parse(JSON.stringify(originalArray)); // Deep copy using JSON methods
originalArray[0][0] = 10; // Modifying an element in the nested array of originalArray
console.log(originalArray); // Output: [[10, 2], [3, 4]]
console.log(clonedArray); // Output: [[1, 2], [3, 4]] (clonedArray is not affected)
```

These cloning methods allow you to duplicate an array while preserving the original array's values without any reference to the original array. Choose the method that best suits your requirements and programming style.

### **Use `const` to Create an Array**

Using const to declare an array in JavaScript is a common practice because it provides benefits in terms of code clarity, preventing accidental reassignment, and promoting immutability.

- When an array is declared with `const`, it indicates that the reference to the array cannot be reassigned to a different array. However, the array itself can still be modified by adding, removing, or modifying elements.
  ```js
  const arr = [1, 2, 3];
  arr.push(4); // OK
  arr = [1, 2, 3, 4]; // Syntax error
  ```
- This is because the value of the array is mutable, but the reference to the array is not.
- Using `const` makes the intention clear that the array reference should remain constant throughout the code. It helps improve code readability and makes it easier for other developers to understand that the array should not be reassigned.
- Declaring an array with `const` helps prevent accidental reassignment of the entire array. If you attempt to assign a new array to a const-declared array variable, it will result in a syntax error. This can help catch errors and enforce the intention to keep the reference constant.

<div align="center">
 <img src="./images/use_const_to_create_array.png"  width="750" height="400">
</div>
