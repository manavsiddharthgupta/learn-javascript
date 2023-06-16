# Understanding Object-Oriented Programming (OOP) in JavaScript

Object-Oriented Programming (OOP) is a powerful programming paradigm that allows developers to structure code in a more organized and modular manner. It provides a way to create objects, which are the building blocks of an application, and define their properties and behaviors.

## Why do we need OOP?

Let's say we want to create a simple application that manages list of users. The `users` should have a `name`, `email` , `age` and `greet` method that prints out a greeting message.

```js
const user1 = {
  name: "Nobita Nobi",
  email: "nobi@doraemon.com",
  age: 10,
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
};

const user2 = {
  name: "Shizuka Minamoto",
  email: "sizuka@doraemon.com",
  age: 10,
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
};

const user3 = {
  name: "Takeshi Goda",
  email: "takes@doraemon.com",
  age: 10,
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
};

...
...
```

If we want to add a new user, we have to create a new object with the `name`, `email`, `age` and `greet` properties. This is not a very efficient way of creating objects. It is also difficult to manage the objects we have created so far.

To solve this problem, we can create a function that creates objects for us.

```js
function createUser(name, email, age) {
  return {
    name: name,
    email: email,
    age: age,
    greet: function () {
      console.log("Hello, my name is " + this.name);
    },
  }
}

const user1 = createUser("Nobita Nobi", "nobi@doraemon.com", 10);
const user2 = createUser("Shizuka Minamoto", "sizuka@doraemon.com", 10);
...
...
```

This is a better approach, but it still has some problems. We are creating a new `greet` function for each object. This is not very efficient. We don't need to create a new function for each object. We can create an object with a `greet` method and then use it for all the objects.

```js
const userFunctions = {
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
};

function createUser(name, email, age) {
  return {
    name: name,
    email: email,
    age: age,
    greet: userFunctions.greet,
  };
}

const user1 = createUser("Nobita Nobi", "nobi@doraemon.com", 10);
user1.greet(); // Hello, my name is Nobita Nobi
```

This is a much better approach. We are creating a single `greet` function and using it for all the objects. We are using reference to the `greet` function instead of creating a new function for each object.

However we still have a problem. Let's say we want to add multiple new method to the `user` object. We have to add it to the `userFunctions` object and then add a reference to it in the `createUser` function. This is not very efficient.

Let's come back to basics.

```js
// Lets create a simple object.
const obj1 = {
  key1: "value1",
  key2: "value2",
};

// create another object obj2

const obj2 = {
  key3: "value3",
  key4: "value4",
};

// i want to access the key1 of obj1 in obj2

console.log(obj2.key1); // undefined

// Here is how we can do it

const obj3 = Object.create(obj1); // create a new object obj3 with all the properties of obj1
console.log(obj3); // { __proto__: { key1: "value1", key2: "value2" } } We can see the __proto__ property. This is the __proto__ property. It contains all the properties of the obj1 object.

// we can access the key1 of obj1 in obj3

console.log(obj3.__proto__); // { key1: "value1", key2: "value2" }
console.log(obj3.key1); // value1

// if you add key1 to obj3, it will override the key1 of obj1

obj3.key1 = "value5";
console.log(obj3.key1); // value5
```

Now let's come back to our example.

```js
const userFunctions = {
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
  is18: function () {
    return this.age >= 18;
  },
};
// let's use what we've learned so far to create a new object
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

Try logging the `user1` object to the console. You will see that it has a `__proto__` property. This is the prototype property. It contains all the properties of the `userFunctions` object.

In official ecmascript documentation `__proto__` is written as `[[Prototype]]`.
In Javascript there is also a `prototype` property which is different from the `__proto__` property. We will discuss about the `prototype` property next.

---
