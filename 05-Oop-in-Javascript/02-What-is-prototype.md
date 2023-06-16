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
  const user = Object.create(createUser.prototype); // here we are using createUser.prototype as the prototype object of user object
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
