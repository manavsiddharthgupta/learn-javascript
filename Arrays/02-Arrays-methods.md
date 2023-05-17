# Arrays Methods

Here are some arrays method that is commonly used in JavaScript:

## **push()**

- The **.push()** method is used to add one or more elements to the end of an array.
- It modifies the original array and returns the new length of the array.
- Example :
  ```js
  let myArray = [1, 2, 3];
  myArray.push(4, 5); // Adds 4 and 5 to the end of the array
  console.log(myArray); // output [1, 2, 3, 4, 5]
  ```

## **pop()**

- The **.pop()** method is used to remove the last element from an array.
- It modifies the original array and returns the removed element.
- Example :
  ```js
  let myArray = [1, 2, 3];
  let poppedElement = myArray.pop(); // Removes 3 from the end of the array
  console.log(myArray); // output [1, 2]
  console.log(poppedElement); // output 3
  ```

## **shift()**

- The **.shift(**) method removes the first element from an array and returns that element.
- It modifies the original array and shifts all other elements down by one index
- Example :
  ```js
  let myArray = [1, 2, 3];
  let shiftedElement = myArray.shift(); // Removes 1 from the beginning of the array
  console.log(myArray); // output [2, 3]
  console.log(shiftedElement); // output 1
  ```

## **unshift()**

- The **.unshift()** method adds one or more elements to the beginning of an array and returns the new length of the array.
- It modifies the original array and shifts all other elements up by one index.
- Example :
  ```js
  let myArray = [1, 2, 3];
  myArray.unshift(4, 5); // Adds 4 and 5 to the beginning of the array
  console.log(myArray); // output [4, 5, 1, 2, 3]
  ```

These are just a few examples of commonly used array methods in JavaScript. There are many more methods available that provide various functionalities for manipulating and working with arrays.
We will learn more about them in the functions.

## **Key Concepts**

**push** and **pop** is faster than **shift** and **unshift** because **shift** and **unshift** have to re-index all the elements in the array.
