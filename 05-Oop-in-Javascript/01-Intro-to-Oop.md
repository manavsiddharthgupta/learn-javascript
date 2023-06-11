# Understanding Object-Oriented Programming (OOP) in JavaScript

Object-Oriented Programming (OOP) is a powerful programming paradigm that allows developers to structure code in a more organized and modular manner. It provides a way to create objects, which are the building blocks of an application, and define their properties and behaviors.

## Why do we need OOP?

Lets say we want to create a simple application that manages list of users. The `users` should have a `name`, `email` , `age` and `greet` method that prints out a greeting message.

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

In official ecmascript documentation `__proto__` is written as `[[Prototype]]`.
In Javascript there is also a `prototype` property which is different from the `__proto__` property. We will discuss about the `prototype` property later.

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

This is a much better approach. We still have not solved the problem fully. We will solve it in the next section.

---

<!-- JavaScript is a multi-paradigm language, which means it supports different programming approaches. It is possible to write code in a functional or object-oriented manner. However, JavaScript is a prototype-based language, which means it doesn't support classes out-of-the-box. This is where OOP comes into play. It allows us to create classes, which are essentially blueprints for creating objects. We can then create objects from these classes using the `new` keyword.

## Classes and Objects

A class is a blueprint for creating objects with pre-defined properties and methods. Let's create a `Person` class with a `name` property and a `greet()` method.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
````

We can now create objects from this class using the `new` keyword.

```js
const john = new Person("John");
john.greet(); // Hello, my name is John
```

## Inheritance

Inheritance is a mechanism that allows us to create new classes from existing classes. The new classes inherit all the properties and methods from the existing classes and can have additional properties and methods of their own. The existing classes are called base classes or parent classes, and the new classes are called derived classes or child classes.

Let's create a `Student` class that inherits from the `Person` class.

```js
class Student extends Person {
  constructor(name, level) {
    super(name);
    this.level = level;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I'm in ${this.level}`);
  }
}
```

The `Student` class inherits the `name` property and the `greet()` method from the `Person` class. It also has its own `level` property and `greet()` method. We can now create objects from this class.

```js
const john = new Student("John", "Beginner");
john.greet(); // Hello, my name is John and I'm in Beginner
```

## Encapsulation

Encapsulation is the process of hiding the internal workings of an application from the rest of the codebase. It allows us to protect the data stored in an object from being modified by accident. We can encapsulate the `level` property in the `Student` class by prepending an underscore to its name. This is a common convention followed by most JavaScript developers.

```js
class Student extends Person {
  constructor(name, level) {
    super(name);
    this._level = level;
  }

  get level() {
    return this._level;
  }

  set level(level) {
    this._level = level;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I'm in ${this.level}`);
  }
}
```

We can now access the `level` property using the `get` and `set` keywords.

```js
const john = new Student("John", "Beginner");
console.log(john.level); // Beginner
john.level = "Intermediate";
john.greet(); // Hello, my name is John and I'm in Intermediate
```

## Polymorphism

Polymorphism is the ability to treat objects of different types in a similar manner. It allows us to perform a single action in different ways. Let's create a `Teacher` class that also inherits from the `Person` class.

```js
class Teacher extends Person {
  constructor(name, subject) {
    super(name);
    this.subject = subject;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I teach ${this.subject}`);
  }
}
```

The `Teacher` class has its own `subject` property and `greet()` method. We can now create objects from this class.

```js
const john = new Teacher("John", "Mathematics");
john.greet(); // Hello, my name is John and I teach Mathematics
```

We can now create an array of `Person` objects and call the `greet()` method on each of them. This is possible because the `Student` and `Teacher` classes inherit from the `Person` class.

```js
const persons = [
  new Student("John", "Beginner"),
  new Teacher("Jane", "Geography"),
];

function printPersons(persons) {
  for (let person of persons) {
    person.greet();
  }
}

printPersons(persons);
// Hello, my name is John and I'm in Beginner
// Hello, my name is Jane and I teach Geography
```

## Conclusion

Object-Oriented Programming (OOP) is a powerful programming paradigm that allows developers to structure code in a more organized and modular manner. It provides a way to create objects, which are the building blocks of an application, and define their properties and behaviors. It also allows us to create new classes from existing classes. The new classes inherit all the properties and methods from the existing classes and can have additional properties and methods of their own. We can also encapsulate the data stored in an object by prepending an underscore to its name. This allows us to protect the data from being modified by accident. Finally, we can treat objects of different types in a similar manner using polymorphism. This allows us to perform a single action in different ways.

## Resources

- [MDN Web Docs: Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) -->
