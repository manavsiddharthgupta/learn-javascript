# Function Inside Object

In javascript objects are key value pairs. The value can be of any type. It can be a string, number, boolean, array, object or even a function. Functions, on the other hand, are reusable blocks of code designed to perform specific tasks. When functions are defined within objects, they become methods and can access the object's properties and other methods.

## Defining a function inside an object

```js
const car = {
  brand: "Toyota",
  model: "Camry",
  year: 2022,
  startEngine: function () {
    console.log("Engine started!");
  },
};
```

In the above example, we have an object named `car` with properties such as `brand`, `model`, and `year`. Additionally, we define a method called `startEngine` using the function syntax within the object. The `startEngine` method simply logs a message to the console.

## Calling a method

To call a method, you need to access the method using the dot notation and then call it using the parenthesis. For example, to call the `startEngine` method, you can use the following code:

```js
car.startEngine(); // Engine started!
```

When you execute the above code, it will print "Engine started!" to the console.

Let's say you want to print the car's brand, model, and year to the console. What you can do is create a method that prints the car's details to the console.

```js
const car = {
  brand: "Toyota",
  model: "Camry",
  year: 2022,
  startEngine: function () {
    console.log("Engine started!");
  },
  printDetails: function () {
    console.log("Car Brand: Toyota, Model: Camry, Year: 2022");
  },
};
```

However, this is not a good approach because you have to hardcode the car's details in the method. What if the car's details change? You will have to update the method as well. A better approach is by accessing the object's properties.

```js
const car = {
  brand: "Toyota",
  model: "Camry",
  year: 2022,
  startEngine: function () {
    console.log("Engine started!");
  },
  printDetails: function () {
    console.log(`Car Brand: ${brand}, Model: ${model}, Year: ${year}`); // Invalid code
  },
};

console.log(car.printDetails()); // ReferenceError: brand is not defined
```

When you execute the above code, you will get a `ReferenceError` because the `brand`, `model`, and `year` variables are not defined. This is because the `printDetails` method is not able to access the object's properties. To access the object's properties, you need to use the `this` keyword.

```js
const car = {
  brand: "Toyota",
  model: "Camry",
  year: 2022,
  startEngine: function () {
    console.log("Engine started!");
  },
  printDetails: function () {
    console.log(
      `Car Brand: ${this.brand}, Model: ${this.model}, Year: ${this.year}`
    );
  },
};
```

## The `this` keyword

The `this` keyword refers to the current object. In the above example, the `this` keyword refers to the `car` object. To access the object's properties, you need to use the `this` keyword followed by the property name.

The behavior of the `this` keyword can vary depending on the context in which it is used. Let's explore the different scenarios in which the `this` keyword can be used and how its value is determined:

### Global context

When the `this` keyword is used in the global context (outside of any function or object), it refers to the global object. In the browser, the global object is the `window` object. In Node.js, the global object is the `global` object. More about global objects click [here](https://developer.mozilla.org/en-US/docs/Glossary/Global_object).

```js
console.log(this); // Output: [object Window] (in browser environment)
```

### Function context

When `this` is used inside a regular function (not an arrow function), its value depends on how the function is invoked:

- If a function is called as a standalone function, `this` refers to the global object (`window` in a browser, `global` in Node.js). For example:

  ```js
  function myFunction() {
    console.log(this);
  }
  myFunction(); // Output: [object Window] (in browser environment)
  ```

- If a function is called as a method of an object, `this` refers to the object the method belongs to. For example:

  ```js
  const car = {
    brand: "Toyota",
    model: "Camry",
    year: 2022,
    printDetails: function () {
      console.log(this);
    },
  };

  car.printDetails(); // Output: { brand: 'Toyota', model: 'Camry', year: 2022, printDetails: [Function: printDetails] }
  ```

- If a function is called using the `new` keyword to create an instance of an `object`, `this` refers to the newly created instance. For example:
  ```js
  function Car(brand, model, year) {
    this.brand = brand;
    this.model = model;
    this.year = year;
    console.log(this);
  }
  const car = new Car("Toyota", "Camry", 2022);
  console.log(car); // Output: Car { brand: 'Toyota', model: 'Camry', year: 2022 }
  ```
  we will learn more about `new` keyword next.

### Arrow function context

Arrow functions behave differently with regard to the `this` keyword. They do not have their own `this` value. Instead, they inherit the `this` value from the surrounding scope (lexical `this` binding). For example:

When using arrow functions as methods inside an object, the lexical binding of `this` ensures that the arrow function does not create its own this context. Instead, it accesses the `this` value from the surrounding scope, which in this case is the enclosing object.

This behavior can be particularly useful when you want to preserve the `this` context from the surrounding scope. It allows you to access the object's properties and methods seamlessly within the arrow function, without the need for additional workarounds such as storing this in a separate variable.

```js
const obj = {
  name: "John",
  sayHello: function () {
    const innerFunction = () => {
      console.log(`Hello, ${this.name}!`); // Hello, John!
    };
    function innerSecFunction() {
      console.log(`Hello, ${this.name}!`); // Hello, undefined! (loses this context)
    }
    innerFunction();
    innerSecFunction();
  },
};

obj.sayHello(); // Output: Hello, John! , Hello, undefined!
```

We define an object `obj` with a property `name` set to the value `"John"`.
The `sayHello` method is defined within `obj`. It is a regular function assigned to the `sayHello` property of the object.
Inside the `sayHello` method, we declare an arrow function named `innerFunction`. Arrow functions inherit the `this` value from their surrounding scope, which in this case is the sayHello method. So, `this` within innerFunction refers to the same `this` as in sayHello, which is the `obj` object. Therefore, `console.log(Hello, ${this.name}!);` will outputs `Hello, John!`.
We declare a regular function named `innerSecFunction` within the `sayHello` method. Regular functions have their own `this` value, determined by the way they are invoked. In this case, `innerSecFunction` is not invoked with any specific context, so its `this` value defaults to the `global object (window in a browser)`. Since the global object does not have a `name` property defined, `console.log(Hello, ${this.name}!);` will outputs `Hello, undefined!`.
We then invoke `innerFunction()`. As it is an arrow function, `this` within `innerFunction` still refers to the `obj` object. Therefore, it will give `Hello, John!`
Next, we invoke `innerSecFunction()`. As a regular function, it creates its own `this` context, which is the `global object (window)`. Since window doesn't have a name property defined, `console.log(Hello, ${this.name}!);` which will give `Hello, undefined!`.

Finally, we call `obj.sayHello()`, which triggers the execution of the `sayHello` method. As a result, `Hello, John!`
`Hello, undefined!`
is logged to the console.

Let's see if you can get the output of the following code:

```js
const obj = {
  name: "John",
  sayHello: () => {
    console.log(`Hello, ${this.name}!`); // Hello, John!
  },
};

obj.sayHello(); // what will be the output?
```
