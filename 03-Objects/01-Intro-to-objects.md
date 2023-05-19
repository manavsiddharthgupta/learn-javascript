# Intro to Objects

## What are Objects

In JavaScript, an object is a collection of key-value pairs, where each key is a string (or a symbol) that uniquely identifies a value. This key-value structure enables you to represent real-world entities or concepts in your code. For example, you could create an object to represent a `person` with properties like `name`, `age`, and `email`.

## Creating Objects

There are several ways to create objects in JavaScript. The most common method is by using object literal notation, which involves defining an object directly in your code using curly braces.

```js
let person = {
  name: "Ben Tennyson",
  age: 21,
  email: "ben@example.com",
};
```

In the above example, we create an object called person with three properties: `name`, `age`, and `email`. The colon separates the key (property name) from its corresponding value.

_The keys in this object (name, age, and email) are indeed strings, although they are not enclosed in quotes. In JavaScript object literals, when keys are unquoted and follow the rules for valid JavaScript identifiers (no spaces, start with a letter, etc.), they are treated as strings._

_So, even though the keys are not explicitly defined as strings with quotes, they are still interpreted as string keys by default. It's a shorthand syntax that JavaScript provides for convenience._

## Accessing Object Properties

Once you have an object, you can access its properties using dot notation or square brackets. Dot notation is the most common and straightforward way to access object properties.

```js
console.log(person.name); // Output: Ben Tennyson
console.log(person.age); // Output: 21
console.log(person.email); // Output: ben@example.com
```

Learn more about Dot VS Bracket notation [here](02-Dot-vs-bracket.md).

## Modifying Object Properties

Objects in JavaScript are mutable, meaning you can modify their properties after they are created. To change the value of a property, simply assign a new value to it using the assignment operator (`=`).

```js
person.age = 19;
console.log(person.age); // Output: 19
```

In the above example, we modify the `age` property of the `person` object and then log the updated value to the console.

## Adding and Removing Object Properties

You can also add new properties to an object or remove existing ones dynamically. To add a new property, simply assign a value to a non-existent property.

```js
person.city = "New York";
console.log(person.city); // Output: New York
```

In this case, we add a `city` property to the `person` object and log its value to the console.

To remove a property from an object, you can use the `delete` keyword followed by the objectname and the property you want to delete.

```js
delete person.email;
console.log(person.email); // Output: undefined
```

Here, we remove the `email` property from the `person` object. Accessing the property afterwards returns `undefined`, indicating that the property no longer exists.

## Conclusion

Objects are an essential part of JavaScript, allowing you to organize and manipulate data in a structured manner. By understanding the basics of objects, you can create more complex programs and handle real-world scenarios effectively. Remember to practice creating, accessing, modifying, and removing properties from objects to solidify your understanding.
