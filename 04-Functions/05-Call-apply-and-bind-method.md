# Call, Apply and Bind Method

The `call`, `apply`, and `bind` methods in JavaScript are used to manipulate the functions and to control the value of `this` within the function, regardless of how the function is originally defined. They are useful when you want to invoke a function in a specific context, **borrow methods from one object to use for another, or create function wrappers**.

By using `call`, `apply`, and `bind`, you can explicitly define the `this` value inside a function, providing more flexibility and control over function execution in JavaScript.

Let's take a an example why we need to use `call`, `apply`, and `bind` methods.

```js
const person1 = {
  name: "John Doe",
  age: 25,
  greet: function () {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  },
};

const person2 = {
  name: "Jane Doe",
  age: 22,
};

person1.greet(); // Hello, my name is John Doe and I am 25 years old.
```

What if we want to use the greet method of person1 for person2?

That is where `call`, `apply`, and `bind` methods come into play. Let's see how we can use them.

## Call Method

The `call` method is used to invoke a function with a specified `this` value. It allows you to borrow a method from one object and use it for another object. The first argument to call sets the `this` value inside the function, and subsequent arguments are passed as separate parameters to the function.

Here is the syntax of the `call` method.

```js
functionName.call(thisArg, arg1, arg2, ...);
// or
object.method.call(thisArg, arg1, arg2, ...);
```

**Example**

```js
const person1 = {
  name: "Ben Tennyson",
  aboutme: function () {
    console.log(`Hello, I am ${this.name}!`);
  },
};

const person2 = {
  name: "Max Tennyson",
};

person1.aboutme.call(person2); // Output: Hello, I am Max Tennyson!
```

In the above example, we have used the `call` method to invoke the `aboutme` function of `person1` for `person2`. The `call` method sets the `this` value of the `aboutme` function to `person2`.

You don't have to create functions inside the object. You can also use the `call` method to invoke a function that is defined outside the object.

```js
const person1 = {
  name: "Ben Tennyson",
};

const person2 = {
  name: "Max Tennyson",
};

function aboutme(hobby, artist) {
  console.log(
    `Hello, I am ${this.name}! My hobby is ${hobby}. My favorite singer is ${artist}.`
  );
}

aboutme.call(person1, "Running", "Drake"); // Output: Hello, I am Ben Tennyson! My hobby is Running. My favorite singer is Drake.

aboutme.call(person2, "Driving"); // Output: Hello, I am Max Tennyson! My hobby is Driving. My favorite singer is undefined.
```

In the above example, we have used the `call` method to invoke the `aboutme` function for `person1` and `person2`. The `call` method sets the `this` value of the `aboutme` function to `person1` and `person2` respectively. The `call` method also passes the `hobby` and `artist` arguments to the `aboutme` function. The `artist` argument is not passed for `person2`, so it is `undefined`.

## Apply Method

The `apply` method is similar to the `call` method. It is used to invoke a function with a specified `this` value. It allows you to borrow a method from one object and use it for another object. The first argument to apply sets the `this` value inside the function, and **the second argument is an array of arguments to be passed to the function**.

Here is the syntax of the `apply` method.

```js
functionName.apply(thisArg, [argsArray]);
// or
object.method.apply(thisArg, [argsArray]);
```

**Example**

```js
const person1 = {
  name: "Ben Tennyson",
  aboutme: function (hobby, artist) {
    console.log(
      `Hello, I am ${this.name}! My hobby is ${hobby}. My favorite singer is ${artist}.`
    );
  },
};

const person2 = {
  name: "Max Tennyson",
};

person1.aboutme.apply(person1, ["Running", "Drake"]); // Output: Hello, I am Ben Tennyson! My hobby is Running. My favorite singer is Drake.

person1.aboutme.apply(person2, ["Driving"]); // Output: Hello, I am Max Tennyson! My hobby is Driving. My favorite singer is undefined.
```

In the above example, we have used the `apply` method to invoke the `aboutme` function of `person1` for `person2`. The `apply` method sets the `this` value of the `aboutme` function to `person2`. The `apply` method also passes the `hobby` and `artist` arguments to the `aboutme` function. The `artist` argument is not passed for `person2`, so it is `undefined`. The `apply` method passes the arguments as an array.

## Bind Method

The `bind` method creates a new function with a specified `this` value and, optionally, pre-set arguments. Unlike `call` and `apply`, `bind` does not immediately execute the function but returns a new function that can be invoked later. It is useful for creating new functions with a fixed `this` value or for creating function wrappers.

Here is the syntax of the `bind` method.

```js
functionName.bind(thisArg, arg1, arg2, ...);
// or
object.method.bind(thisArg, arg1, arg2, ...);
```

**Example**

```js
const person1 = {
  name: "Gwen Tennyson",
  aboutme: function (hobby, artist) {
    console.log(
      `Hello, I am ${this.name}! My hobby is ${hobby}. My favorite singer is ${artist}.`
    );
  },
};

const person2 = {
  name: "Kevin Levin",
};

const aboutmePerson1 = person1.aboutme.bind(person1, "Hiking", "Ariana Grande");
aboutmePerson1(); // Output: Hello, I am Gwen Tennyson! My hobby is Hiking. My favorite singer is Ariana Grande.

const aboutmePerson2 = person1.aboutme.bind(person2, "Biking", "Eminem");.
aboutmePerson2(); // Output: Hello, I am Kevin Levin! My hobby is Biking. My favorite singer is Eminem.
```

In the above example, we have used the `bind` method to create a new function `aboutmePerson1` with a fixed `this` value of `person1`. The `bind` method also passes the `hobby` and `artist` arguments to the `aboutme` function. The `aboutmePerson1` function can be invoked later.

In contrast, the `call` and `apply` methods immediately invoke the function. The `bind` method is useful for creating function wrappers.

Let's see if you can get the output of the following code:

```js
const obj = {
  name: "Alex Smith",
  aboutme: function () {
    console.log(`Hello, I am ${this.name}!`);
  },
};

obj.aboutme.call(); // what is the output?
```
