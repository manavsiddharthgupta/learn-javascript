# Dot VS Bracket

In JavaScript, both dot notation and bracket notation are used to access and manipulate object properties.

## Dot Notation:

Dot notation is the most common and straightforward way to access object properties. It uses a period (.) followed by the property name to access the value. Here's an example:

```js
let person = {
  name: "Ben Tennyson",
  age: 21,
  email: "ben@example.com",
};

console.log(person.name); // Output: Ben Tennyson
console.log(person.age); // Output: 21
console.log(person.email); // Output: ben@example.com
```

In this example, dot notation is used to access the properties `name`, `age`, and `email` of the `person` object.

## Bracket Notation:

Bracket notation involves using square brackets ([]) to access object properties. It is particularly useful when the property name is dynamic or contains special characters. Here's an example:

```js
let person = {
  name: "Ben Tennyson",
  age: 21,
  email: "ben@example.com",
};

let propertyName = "name";
console.log(person[propertyName]); // Output: Ben Tennyson

propertyName = "age";
console.log(person[propertyName]); // Output: 21
```

In this example, bracket notation is used to access the properties name and age of the person object. The property name is stored in the propertyName variable, which allows for dynamic property access.

Bracket notation is also useful when working with object properties that have special characters, spaces, or when using symbols as keys. Here's an example:

```js
let person = {
  "first name": "Ben",
  "last name": "Tennyson",
  "email-address": "ben@example.com",
  "@username": "bentennyson",
  1: "Numeric Key",
};

console.log(person["first name"]); // Output: Ben
console.log(person["last name"]); // Output: Tennyson
console.log(person["email-address"]); // Output: ben@example.com
console.log(person["@username"]); // Output: bentennyson
console.log(person[1]); // Output: Numeric Key
```

In this case, bracket notation is used to access properties with special characters or spaces in their names.

Both dot notation and bracket notation are valid and widely used in JavaScript. The choice between them depends on the specific requirements of your code, such as whether you need dynamic property access or the property name contains special characters.
