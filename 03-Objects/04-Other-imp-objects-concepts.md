# Here are some other objects concepts

## Computed Properties

Computed properties in JavaScript allow you to dynamically set object property names using an expression within square brackets. This feature provides flexibility and allows you to create object properties based on variables or computed values. Let's dive into how computed properties work and explore some examples.

```js
const firstKey = "firstName";
const secondKey = "lastName";

const firstValue = "Ben";
const secondValue = "Tennyson";

const person = {
  [firsKey]: firstValue,
  [secondKey]: secondValue,
};

console.log(person); //  Output: { firstName: 'Ben', lastName: 'Tennyson' }
```

## How to Copy/Clone Objects

We can't copy objects in JavaScript the same way we copy primitive values. By assigning an object to a new variable, we are only creating a reference to the original object. This means that any changes made to the new object will also affect the original object. learn more about primitive vs reference data types [here](../02-Arrays/03-Primitive-vs-reference-datatypes.md).

To clone or copy objects in JavaScript, you have a few options. Let's explore three commonly used methods.

### 1. **The Spread Operator**

The spread syntax (...) is a concise way to copy the properties of an object into a new object. Here's an example:

```js
const originalObj = { foo: "bar", baz: "qux" };

const clonedObj = { ...originalObj };

console.log(clonedObj); // Output: { foo: 'bar', baz: 'qux' }
```

In this example, the spread syntax is used to create a new object `clonedObj` with the same properties as `originalObj`. The properties are shallow copied, meaning any nested objects or arrays are still references to the original objects. Learn more about shallow vs deep copying [here](../02-Arrays/03-Primitive-vs-reference-datatypes.md).

### 2. **The Object.assign() Method**

The `Object.assign()` method is another way to copy an object. It copies the enumerable properties from one or more source objects to a target object. Here's an example:

```js
const originalObj = { foo: "bar", baz: "qux" };

const clonedObj = Object.assign({}, originalObj);

console.log(clonedObj); // Output: { foo: 'bar', baz: 'qux' }
```

In this example, `Object.assign()` is used to copy the properties from `originalObj `to an empty target object `{}`. The result is a new object `clonedObj` with the same properties as `originalObj`.
