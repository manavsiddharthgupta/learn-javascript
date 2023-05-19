# How to Iterarte Objects

Objects in JavaScript are collections of key-value pairs, and being able to iterate over their properties allows you to access and manipulate data efficiently. In this article, we will explore different methods for iterating objects and provide examples to help you grasp the concepts.

## The for...in Loop

The for...in loop is a simple and commonly used method for iterating over the properties of an object. It allows you to loop through each enumerable property of an object and perform operations on them. Here's an example:

```js
let person = {
  name: "Ben Tennyson",
  age: 21,
  email: "ben@example.com",
};

for (let key in person) {
  console.log(key + ": " + person[key]);
}
```

You can learn more about for...in loop [here](../01-Introduction%20to%20Javascript/06-Control-flow.md).

## The Object.keys() Method

The `Object.keys()` method returns an array containing the enumerable property names of an object. This array can be easily iterated using various looping techniques. Here's an example:

```js
let person = {
  name: "John Doe",
  age: 25,
  email: "johndoe@example.com",
};

for (let key of Object.keys(person)) {
  console.log(key + ": " + person[key]);
}
```

In this example, `Object.keys(person)` returns an array of property names (`name`, `age`, `email`). We then use the `for of loop` to iterate over this array. The loop variable `key` represents each property name, and `person[key]` gives us access to the corresponding value.

## Key Concepts

Remember that the order of object properties is not guaranteed in JavaScript. Properties may be iterated in a different order than they were defined.
