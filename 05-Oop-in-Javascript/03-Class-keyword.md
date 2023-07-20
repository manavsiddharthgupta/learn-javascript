# Class Keyword

The `class` keyword is used to define a new class, which serves as a blueprint for creating objects with shared properties and methods. It provides a more structured and object-oriented approach to organizing code. The `class` keyword was introduced in *ECMAScript 6 (ES6)* to simplify the process of creating constructor functions and [prototypes](./02-What-is-prototype.md).


1. Let's create a class using the `class` keyword.
  To create a class, you use the `class` keyword followed by the name of the class. The class name should begin with an uppercase letter by convention (e.g., `class MyClass`). The class body is enclosed in curly braces `{}`.
```js
class MyClass {
  // Class body goes here
}
```
2. Constructor Method
  The constructor method is a special method that is called when you create a new instance of the class using the `new` keyword. It is used to initialize object properties and perform setup operations.
```js
class MyClass {
  constructor(param1, param2) {
    this.property1 = param1;
    this.property2 = param2;
  }
}
```

3. Class Methods
  Class methods are functions that are defined inside the class body. They are used to perform operations on the class properties. Class methods are similar to prototype methods, but they are defined inside the class body using the `method` keyword.
```js
class MyClass {
  constructor(param1, param2) {
    this.property1 = param1;
    this.property2 = param2;
  }

  method1() {
    // code goes here
  }

  method2() {
    // code goes here
  }
}
```
4. Creating an Instance of a Class
  To create an instance of a class, you use the `new` keyword followed by the class name and any arguments required by the constructor method. Learn about `new` keyword in [this section](./02-What-is-prototype.md#new-keyword).
```js
const myObj1 = new MyClass("value1", "value2");
const myObj2 = new MyClass("value3", "value4");
```
Let's recreate our application using `class` keyword.

```js
class CreateUser {
  constructor(name, email, age) {
    this.name = name;
    this.email = email;
    this.age = age;
  }

  greet() {
    console.log("Hello, my name is " + this.name);
  }

  is18() {
    return this.age >= 18;
  }
}

// Create an instance using the 'new' keyword
const user1 = new CreateUser("Nobita Nobi", "nobi@doraemon.com", 10);
const user2 = new CreateUser("Shizuka Minamoto", "sizuka@doraemon.com", 10);

user1.greet(); // Hello, my name is Nobita Nobi
user2.greet(); // Hello, my name is Shizuka Minamoto

console.log(Object.getPrototypeOf(user1)); // Outputs: CreateUser {greet: function, is18: function}
```
Here, we have created a class called `CreateUser` with a constructor method that takes three parameters: `name`, `email`, and `age`. The constructor method is used to initialize the object properties. We have also defined two class methods: `greet()` and `is18()`. The `greet()` method is used to print a greeting message to the console, and the `is18()` method is used to check if the user is 18 years or older. These methods are similar to the prototype methods we created in the previous section.

## Inheritance

Inheritance is a mechanism that allows you to create a new class from an existing class. The new class inherits all the properties and methods of the existing class and can add its own unique properties and methods. Inheritance is one of the core concepts of object-oriented programming (OOP).

Inheritance allows you to create a hierarchy of classes. The classes at the top of the hierarchy are called parent classes or base classes. The classes at the bottom of the hierarchy are called child classes or derived classes. A child class inherits all the properties and methods of its parent class and can add its own unique properties and methods.

`super` keyword is used to call the constructor of the parent class. It is used to access the parent's properties and methods from the child class.

You can create a subclass that inherits properties and methods from a parent class using the `extends` keyword.
```js
class ParentClass {
  // Parent class properties and methods
}

class ChildClass extends ParentClass {
  // Child class properties and methods
}
```

Let's create a subclass called `CreateAdmin` that inherits properties and methods from the `CreateUser` class.

```js
class CreateUser {
  constructor(name, email, age) {
    this.name = name;
    this.email = email;
    this.age = age;
  }

  greet() {
    console.log("Hello, my name is " + this.name);
  }

  is18() {
    return this.age >= 18;
  }
}

class CreateAdmin extends CreateUser {
  constructor(name, email, age, role) {
    super(name, email, age); // call the constructor of the parent class
    this.role = role; // add a new property
  }

  isAdmin() {
    return this.role === "admin";
  } // add a new method
}

// Create an instance using the 'new' keyword
const admin1 = new CreateAdmin("Doraemon", "doraemon@dora.com", 100, "admin");

admin1.greet(); // Hello, my name is Doraemon
console.log(admin1.isAdmin()); // true
console.log(Object.getPrototypeOf(admin1)); // Outputs: CreateAdmin {isAdmin: function}
```