# Objects and Arrays

## Objects inside arrays

Useful for storing data that is related to each other.

```js
const user = [
  {
    userId: 1,
    firstName: "John",
    lastName: "Doe",
    age: 30,
    gender: "male",
  },
  {
    userId: 2,
    firstName: "Alex",
    lastName: "Mair",
    age: 28,
    gender: "female",
  },
  {
    userId: 3,
    firstName: "Max",
    lastName: "Tennyson",
    age: 10,
    gender: "male",
  },
];
```

## Desctructuring

Object and array destructuring are powerful features that allow you to extract values from objects and arrays into individual variables. The destructuring syntax allows us to extract values from arrays or objects and assign them to variables in a single line of code.

### Object destructuring

Object destructuring allows you to extract values from an object and assign them to variables with corresponding names. Consider the following example:

```js
const person = {
  name: "John Doe",
  age: 25,
  email: "johndoe@example.com",
};

const { name, age, email } = person;

console.log(name); // Output: John Doe
console.log(age); // Output: 25
console.log(email); // Output: johndoe@example.com
```

In this example, we have an object `person` with properties such as `name`, `age`, and `email`. Using object destructuring, we extract the values of those properties into individual variables with the same names. This allows us to access and use the data conveniently.

You can also assign new variable names during object destructuring by using the `:` symbol. Here's an example:

```js
const person = {
  name: "John Doe",
  age: 25,
  email: "johndoe@example.com",
};

const { name: fullName, age, email } = person;

console.log(fullName); // Output: John Doe
console.log(age); // Output: 25
console.log(email); // Output: johndoe@example.com
```

In this case, we assign the value of the `name` property to a new variable `fullName` during the destructuring process.

**Using spread operator in object destructuring**

In object destructuring, the spread operator can be used to assign the remaining properties of an object to a new object. Here's an example:

```js
const person = {
  name: "John Doe",
  age: 25,
  email: "johndoe@example.com",
  country: "USA",
};

const { name, age, ...rest } = person;

console.log(name); // Output: John Doe
console.log(age); // Output: 25
console.log(rest); // Output: { email: "johndoe@example.com", country: "USA" }
```

### Array destructuring

Array destructuring allows you to extract values from an array and assign them to variables with corresponding names. Consider the following example:

```js
const rgb = [255, 200, 0];
const [red, green, blue] = rgb;
console.log(red); // Output: 255
```

**Using spread operator in array destructuring**

In array destructuring, the spread operator can be used to assign the remaining elements of an array to a new array. Here's an example:

```js
const numbers = [1, 2, 3, 4, 5];

const [first, second, ...rest] = numbers;

console.log(first); // Output: 1
console.log(second); // Output: 2
console.log(rest); // Output: [3, 4, 5]
```

### **Nested destructuring**

Nested destructuring takes this concept further by allowing us to destructure values from nested objects or arrays. It enables us to extract deeply nested values in a concise and readable manner. Let's take a look at an example to better understand how it works:

```js
const user = [
  {
    userId: 1,
    firstName: "John",
    lastName: "Doe",
    age: 30,
    gender: "male",
  },
  {
    userId: 2,
    firstName: "Alex",
    lastName: "Mair",
    age: 28,
    gender: "female",
  },
  {
    userId: 3,
    firstName: "Max",
    lastName: "Tennyson",
    age: 10,
    gender: "male",
  },
];

const [{ userId: id, firstName }, user2, { userId, ...userData }] = user;

console.log(id, firstName); // 1 John
console.log(user2); // { userId: 2, firstName: 'Alex', lastName: 'Mair', age: 28, gender: 'female'}
console.log(userData); // { firstName: 'Max', lastName: 'Tennyson', age: 10, gender: 'male' }
```
