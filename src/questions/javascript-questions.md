---
title: JavaScript Questions
layout: layouts/page.njk
permalink: /questions/javascript-questions/index.html
---

- **Explain event delegation.**

  ***

  Explain event propagation first. There are three phases: Capture, target, and bubble.

  Event delegation is when a parent element adds event listeners to its children. The event listener will fire anytime an event is triggered on the child element, due to the event bubbling.

  > Event delegation can be extremely useful when you want to automatically set an event listener on child elements. For example, say you want to add an event listener to all the \<li> elements of an \<ul>. However, the unordered list is dynamically generated, based on some data received from an API call. It would be impossible to attach an event handler to each \<li> element individually, but you could attach it to the \<ul> element and it would be delegated to each of the child \<li> elements!

  ***

- **Explain how `this` works in JavaScript.**

  ***

  A property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object and in strict mode can be any value.

  | Context  | Strict         | Non-strict     |
  | -------- | -------------- | -------------- |
  | Global   | global object  | global object  |
  | Function | undefined      | global object  |
  | Class    | regular object | regular object |

  \* To set the value of this to a particular value when calling a function, use call(), or apply() as in the examples below. They will pass a object as this to functions.

  \* Within a class constructor, this is a regular object. All non-static methods within the class are added to the prototype of this

  ECMAScript 5 introduced **Function.prototype.bind().** Calling f.bind(someObject) creates a new function with the same body and scope as f, but where this occurs in the original function, in the new function it is permanently bound to the first argument of bind, regardless of how the function is being used.

  **_this_ in Decalred functions depends how functions are called**

  - **Can you give an example of one of the ways that working with `this` has changed in ES6?**

    ***

    ES2015 introduced arrow functions which don't provide their own this binding (it retains the this value of the enclosing lexical context). Note: if _this_ arg is passed to call, bind, or apply on invocation of an arrow function it will be ignored. You can still prepend arguments to the call, but the first argument (thisArg) should be set to null.

    ```javascript
    var a = "Global";

    function whatsThis() {
      return this.a; // The value of this is dependent on how the function is called
    }

    whatsThis(); // 'Global' as this in the function isn't set, so it defaults to the global/window object
    whatsThis.call(obj); // 'Custom' as this in the function is set to obj
    whatsThis.apply(obj); // 'Custom' as this in the function is set to obj
    ```

    ***

- **Explain how prototypal inheritance works.**

  ***

  A prototype is a characteristic of an object, and specifically resolution of a property access. Think about a prototype as a linkage between two objects; the linkage is hidden behind the scenes, though there are ways to expose and observe it. This prototype linkage occurs when an object is created; it’s linked to another object that already exists. A series of objects linked together via prototypes is called the “prototype chain.”

  ```javascript
  var homework = { topic: "JS" };
  homework.toString(); // example of prototype
  // in this case prototype chain: homeword -> object.prototype -> null
  ```

  **Inheritence**: use ES6 `var a = object.create(obj)` to create a inherited object. You can shadow methods belongs to original obj. prototype chain: a -> obj. (created a prototype)

  Use the _new_ operator to create an instance of doSomething() based on this prototype, which is different with object.create.

  \*hasOwnProperty is the only thing in JavaScript which deals with properties and does not traverse the prototype chain.

  ***

- **What's the difference between a variable that is: `null`, `undefined` or undeclared**

  ***

  _undefined_ is a variable that has been declared but no value exists and is a type of itself ‘undefined’.

  _null_ is a value of a variable and is a type of object.

  _undeclared_ variables is a variable that has been declared without ‘var’

  ***

  - **How would you go about checking for any of these states?**

    ***

    We use `console.log();` and `typeOf` to check if a variable is undefined or null.

    undeclared variables:

    In ECMAScript 5, this behavior was changed for strict mode. Assignment to an unqualified identifier in strict mode will result in a ReferenceError, to avoid the accidental creation of properties on the global object.

    Note that the implication of the above, is that, contrary to popular misinformation, JavaScript does not have implicit or undeclared variables, it merely has a syntax that looks like it does.

    ***

- **What is a closure, and how/why would you use one?**

  ***

  A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

  an inner function that has access to the outer (enclosing) function’s variables — scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function’s variables, and it has access to the global variables. Read here and at MDN. You use one when you later need access to the variables of a function that has returned alread

  Example of closure.

  ```javascript
  function init() {
    var name = "Mozilla"; // name is a local variable created by init
    function displayName() {
      // displayName() is the inner function, a closure
      // displayName is closed over name
      alert(name); // use variable declared in the parent function
    }
    displayName();
  }

  init();
  ```

  PS:

  POLE (The Principle Of Least Exposure)

  Prevent:

  1. Naming Collisions

  2. Unexpected Behavior: if you expose variables/func- tions whose usage is otherwise private to a piece of the program, it allows other developers to use them in ways you didn’t intend, which can violate expected behavior and cause bugs.

  3. UnintendedDependency:ifyouexposevariables/func- tions unnecessarily, it invites other developers to use and depend on those otherwise private pieces. While that doesn’t break your program today,

  POLE encourages us to use block (and function) scoping to limit the scope exposure of variables. This helps keep code understandable and maintainable, and helps avoid many scoping pitfalls (i.e., name collision, etc.).
  Closure builds on this approach: for variables we need to use over time, instead of placing them in larger outer scopes, we can encapsulate (more narrowly scope) them but still preserve access from inside functions, for broader use. Functions remember these referenced scoped variables via closure.

  ***

- **What language constructions do you use for iterating over object properties and array items?**

  ***

  ```javascript
  const arr = [1, 2, 3];
  const obj = { a: a, b: b };
  ```

  For loop

  ```javascript
  for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
  ```

  For in

  ```javascript
  for (const name in obj) {
    console.log(obj[name]);
  }
  ```

  For of

  ```javascript
  for (const element of arr) {
    console.log(obj[element]);
  }
  ```

  Array iterator

  Array.prototype.forEach() is similar to for...in, but only iterates over an object’s own properties.

  Array.prototype.every(): returns true if the callback returns true for every element.

  Array.prototype.some(): returns true if the callback returns true for at least one element.

  Array transformer

  Array.prototype.map(callback, [thisValue]): Each output array element is the result of applying callback to an input element.

  Array.prototype.filter(callback, [thisValue]): The output array contains only those input elements for which callback returns true.

  Reduce

  Array.prototype.reduce(callback, [initialValue]): Compute a value by applying callback to pairs (previousElement, currentElement) of array elements.

  Array.prototype.reduceRight(callback, [initialValue]): Same as reduce(), but from right to left.

  object.values()

  object.key()

  object.getOwnPropertyNames() includes prototype ones

  ***

- **Can you describe the main difference between the `Array.forEach()` loop and `Array.map()` methods and why you would pick one versus the other?**

  ***

  |             | map       | forEach   |
  | ----------- | --------- | --------- |
  | Return type | new array | undefiend |
  | Mutability  | immutable | mutable   |
  | Speed       | faster    |           |

  ***

- **What's a typical use case for anonymous functions?**

  ***

  Function expression and IIFE

  The main difference between a function expression and a function declaration is the function name, which can be omitted in function expressions to create anonymous functions.

  ***

- **What's the difference between host objects and native objects?**

  ***

  Host objects:
  Objects added by code hosted enviroments, for example, `console`.

  Native objects:
  Javascript built in objects, regardless the host enviroment. for example, Math object, Array objects.

  ***

- **Explain the difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?**

  ***

  `function Person(){}`: function declaration, it is a named function.It gets registered into the global namespace.

  `var person = Person()`: Function expression, invoke a function and assign the return value of Person function to person.

  `var person = new Person()`: Use function constructor to create a instance of function declaration;

  ***

- **Explain the differences on the usage of `foo` between `function foo() {}` and `var foo = function() {}`**

  ***

  Named function vs variable foo holds anomynous function address

  Difference in hoisting.

  This different, but closure is the same.

  A function defined by a function expression or by a function declaration inherits the current scope

  ***

- Can you explain what `Function.call` and `Function.apply` do? What's the notable difference between the two?
- Explain `Function.prototype.bind`.
- What's the difference between feature detection, feature inference, and using the UA string?
- Explain "hoisting".
- Describe event bubbling.
- Describe event capturing.
- What's the difference between an "attribute" and a "property"?
- What are the pros and cons of extending built-in JavaScript objects?
- What is the difference between `==` and `===`?
- Explain the same-origin policy with regards to JavaScript.
- Why is it called a Ternary operator, what does the word "Ternary" indicate?
- What is strict mode? What are some of the advantages/disadvantages of using it?
- What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
- What tools and techniques do you use debugging JavaScript code?
- Explain the difference between mutable and immutable objects.
  - What is an example of an immutable object in JavaScript?
  - What are the pros and cons of immutability?
  - How can you achieve immutability in your own code?
- Explain the difference between synchronous and asynchronous functions.
- What is event loop?
  - What is the difference between call stack and task queue?
- What are the differences between variables created using `let`, `var` or `const`?
- What are the differences between ES6 class and ES5 function constructors?
- Can you offer a use case for the new arrow `=>` function syntax? How does this new syntax differ from other functions?
- What advantage is there for using the arrow syntax for a method in a constructor?
- What is the definition of a higher-order function?
- Can you give an example for destructuring an object or an array?
- Can you give an example of generating a string with ES6 Template Literals?
- Can you give an example of a curry function and why this syntax offers an advantage?
- What are the benefits of using `spread syntax` and how is it different from `rest syntax`?
- How can you share code between files?
- Why you might want to create static class members?
- What is the difference between `while` and `do-while` loops in JavaScript?
- What is a promise? Where and how would you use promise?

## Coding questions

- Make this work:

```javascript
duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]
```

- Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`
- What will be returned by each of these?

```javascript
console.log("hello" || "world");
console.log("foo" && "bar");
```

- Write an immediately invoked function expression (IIFE)
