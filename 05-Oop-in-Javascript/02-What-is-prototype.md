# What is Prototype

In JavaScript function also act as an object.

```js
function greet() {
  console.log("Hello");
}

console.log(greet.name); // Outputs: greet

// you can also add properties to function

greet.language = "English";

console.log(greet.language); // Outputs: English
```

Now, Every function has a property called `prototype`. This `prototype` property is an object (referred as prototype object) which has a constructor property by default. This constructor property points back to the function on which prototype object is a property. Let's understand this with an example.

```js
function greet() {
  console.log("Hello");
}

console.log(greet.prototype); // Outputs: Object {constructor: function}

console.log(greet.prototype.constructor); // Outputs: function greet()

// here greet.prototype.constructor points back to the function greet()
```

Only functions have the prototype property. You can also add properties to the prototype object.

```js
function greet() {
  console.log("Hello");
}

greet.prototype.language = "English";

console.log(greet.prototype.language); // Outputs: English

// You can also add methods to the prototype object

greet.prototype.wish = function () {
  console.log("Good Morning");
};

greet.prototype.wish(); // Outputs: Good Morning
```

## `__proto__` and prototype

Now, let's recall the `__proto__` property used in developing the simple application that manages list of users. Click [here](../05-Oop-in-Javascript/01-Intro-to-Oop.md#why-do-we-need-oop?) to learn about `__proto__` property.

```js
const userFunctions = {
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
  is18: function () {
    return this.age >= 18;
  },
};
// using object.create() to create a new object that create __proto__ property
function createUser(name, email, age) {
  const user = Object.create(userFunctions);
  user.name = name;
  user.email = email;
  user.age = age;
  return user;
}

const user1 = createUser("Nobita Nobi", "nobi@doraemon.com", 10);
user1.greet(); // Hello, my name is Nobita Nobi
console.log(user1.is18()); // false
```

Here, `userFunctions` is the prototype object of `user1` object. `user1` object has a `__proto__` property which points to the `userFunctions` object.

Now, We know that `createUser` function should have a `prototype` property. Let' see if it has a `prototype` property.

```js
function createUser(name, email, age) {
  const user = Object.create(userFunctions);
  user.name = name;
  user.email = email;
  user.age = age;
  return user;
}

console.log(createUser.prototype); // Outputs: Object {constructor: function}
```

We are sure that `createUser` function has a `prototype` property. So we don't need `userFunctions` object to be the prototype object of `user1` object. We can use `createUser.prototype.somemethod = () => {}` to add methods in the prototype object of createUser function.

```js
function createUser(name, email, age) {
  const user = Object.create(createUser.prototype); // here we are using createUser.prototype as the prototype object of user object.
  user.name = name;
  user.email = email;
  user.age = age;
  return user;
}

createUser.prototype.greet = function () {
  console.log("Hello, my name is " + this.name);
};

createUser.prototype.is18 = function () {
  return this.age >= 18;
};

const user1 = createUser("Nobita Nobi", "nobi@doraemon.com", 10);
const user2 = createUser("Shizuka Minamoto", "sizuka@doraemon.com", 10);

user1.greet(); // Hello, my name is Nobita Nobi
user2.greet(); // Hello, my name is Shizuka Minamoto

console.log(user1.is18()); // false
console.log(user2.is18()); // false

// Now, if we console.log(user1.__proto__) we will get the same output as console.log(createUser.prototype).

console.log(user1.__proto__); // Outputs: Object {greet: function, is18: function}
```

Here we have removed the `userFunctions` object and used `createUser.prototype` as the prototype object of `user1` and `user2` object. Now, `user1` and `user2` object has a `__proto__` property which points to the `createUser.prototype` object. Our application is more efficient now since we have removed the `userFunctions` object.

When we use `const user = Object.create(createUser.prototype);` to create a new object, the `__proto__` property of the newly created object points to the `createUser.prototype` object. So, the newly created object inherits all the properties and methods of the `createUser.prototype` object. This is called `prototypal inheritance`.

## `new` keyword

In JavaScript, the `new` keyword is used to create an instance of an object from a function. When used with a function, the new keyword performs the following actions:

- The `new` keyword creates a new object based on a blueprint called a constructor function.

- It sets up the newly created object with some initial values and behaviors defined in the constructor function.

- It allows us to create multiple instances (objects) that share the same structure and behaviors defined by the constructor function.

- The `new` keyword is used when we want to create objects using a constructor function instead of object literals or factory functions.

- It automatically sets up the object's internal properties and links it to the constructor function's prototype for inheriting properties and methods.

- We use the `new` keyword by placing it before the constructor function and calling it like a regular function to create a new object.

Let's update our application with `new` keyword.

```js
function CreateUser(name, email, age) {
  // const user = Object.create(createUser.prototype); // here we are using createUser.prototype as the prototype object of user object
  // user.name = name;
  // user.email = email;
  // user.age = age;
  // return user;

  // instead of above code we can use new keyword
  this.name = name;
  this.email = email;
  this.age = age;
} // this function will act as a constructor function

CreateUser.prototype.greet = function () {
  console.log("Hello, my name is " + this.name);
};

CreateUser.prototype.is18 = function () {
  return this.age >= 18;
};

// Create an instance using the 'new' keyword
const user1 = new CreateUser("Nobita Nobi", "nobi@doraemon.com", 10);
const user2 = new CreateUser("Shizuka Minamoto", "sizuka@doraemon.com", 10);

user1.greet(); // Hello, my name is Nobita Nobi
user2.greet(); // Hello, my name is Shizuka Minamoto

console.log(user1.is18()); // false
console.log(user2.is18()); // false

// if we console.log(user1.__proto__) we will get the same output as console.log(createUser.prototype).

console.log(user1.__proto__); // Outputs: Object {greet: function, is18: function}
```

### hasOwnProperty()

`hasOwnProperty` is a method in JavaScript that allows you to check if an object has a specific property directly on itself, without considering properties inherited from its prototype chain.

```js
function CreateUser(name, email, age) {
  this.name = name;
  this.email = email;
  this.age = age;
}

CreateUser.prototype.greet = function () {
  console.log("Hello, my name is " + this.name);
};

CreateUser.prototype.is18 = function () {
  return this.age >= 18;
};

const user1 = new CreateUser("Nobita Nobi", "nobi@doraemon.com", 10);

console.log(user1.hasOwnProperty("name")); // true
console.log(user1.hasOwnProperty("greet")); // false
console.log(user1.hasOwnProperty("is18")); // false
```

Here, `user1` object has a `name` property directly on itself, so `user1.hasOwnProperty("name")` returns `true`. But `user1` object doesn't have `greet` and `is18` property directly on itself, so `user1.hasOwnProperty("greet")` and `user1.hasOwnProperty("is18")` returns `false`.

### more about Prototype

Let's create an array.

```js
const arr = [1, 2, 3, 4, 5];
```

Now, we can use array methods to manipulate the array.

```js
arr.push(6);
arr.forEach((item) => console.log(item));
```

But how is this possible? Beacuse we know that only function has prototype property. So, how can an array has prototype property?

The answer is, `Array` is a constructor function. When we create an array using `[]` or `new Array()`, JavaScript engine creates an array object using `Array` constructor function. So, `Array` constructor function is the blueprint of an array object. And `Array.prototype` is the prototype object of an array object. So, when we create an array using `[]` or `new Array()`, JavaScript engine creates an array object using `Array` constructor function and sets `Array.prototype` as the prototype object of the newly created array object. That's why we can use array methods to manipulate the array.

```js
const arr1 = [1, 2, 3, 4, 5];

// or

const arr2 = new Array(1, 2, 3, 4, 5);

console.log(arr1.__proto__ === Array.prototype); // true
console.log(arr2.__proto__ === Array.prototype); // true

console.log(Array.prototype); // [constructor: ƒ, concat: ƒ, copyWithin: ƒ, fill: ƒ, find: ƒ, …]

// we can also use Object.getPrototypeOf() method to get the prototype object of an array object

console.log(Object.getPrototypeOf(arr1)); // [constructor: ƒ, concat: ƒ, copyWithin: ƒ, fill: ƒ, find: ƒ, …]
```
