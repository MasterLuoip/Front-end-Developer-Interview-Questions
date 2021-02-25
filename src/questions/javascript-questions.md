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

  ***

  apply: invoke the function with arguments as an array.

  call: invoke the function with arguments splited by commas.

  ***

- Explain `Function.prototype.bind`.

  ***

  The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called

  ***

- What's the difference between feature detection, feature inference, and using the UA string?

  ***

  Feature detection checks a feature for existence, e.g.:

  Feature inference checks for a feature just like feature detection, but uses another function because it assumes it will also exist, e.g.:

  (Deprecated) Checking the UA string is an old practice and should not be used anymore. You keep changing the UA checks and never benefit from newly implemented features, e.g.:

  ***

- Explain "hoisting".

  ***

  Conceptually, for example, a strict definition of hoisting suggests that variable and function declarations are physically moved to the top of your code, but this is not in fact what happens. Instead, the variable and function declarations are put into memory during the compile phase, but stay exactly where you typed them in your code.

  JavaScript only hoists declarations, not initializations. If a variable is declared and initialized after using it, the value will be undefined. For example:

  ```javascript
  console.log(num); // Returns undefined, as only declaration was hoisted, no initialization has happened at this stage throw reference error
  var num; // Declaration
  num = 6; // Initialization
  ```

  ***

- Describe event bubbling.

  ***

  When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

  The most deeply nested element that caused the event is called a **target element**, accessible as event.target.

  But any handler may decide that the event has been fully processed and stop the bubbling.

  The method for it is event.stopPropagation().

  ***

- Describe event capturing.

  ***

  The standard DOM Events describes 3 phases of event propagation:

  Capturing phase – the event goes down to the element.

  Target phase – the event reached the target element.

  Bubbling phase – the event bubbles up from the element.

  ![image](https://miro.medium.com/max/640/1*QXDzDRLYkUwbVvVGBPTWHw.png)

  ***

- What's the difference between an "attribute" and a "property"?

  ***

  attribute is html attribute. property is DOM property.

  `<input type="text" value="0">`

  vs

  ```javascript
  const input = document.querySelector("input");
  console.log(input.value); // talking to the Dom property not attribute
  ```

  Update DOM won't update attribute. Two values can be different.

  Use `setAttribute` can change attribute value, and property as well.

  The DOM is optimized and fast, so using something like value over setAttribute makes much more sense.

  ***

- What are the pros and cons of extending built-in JavaScript objects?

  ***

  props:

  1. one set up, easy to use in the future

  cons:

  1. But when you change the behaviour of something that is also used by other code there is a risk you will break that other code.

  2. When it comes adding methods to the object and array classes in javascript, the risk of breaking something is very high, due to how javascript works.

  ***

- What is the difference between `==` and `===`?

  ***

  '==' allows coercion, left side will coersed firstly then compare.

  '===' is strict compare, doesn't allow coersion.

  ***

- Explain the same-origin policy with regards to JavaScript.

  ***

  The same-origin policy is a critical security mechanism that restricts how a document or script loaded from one origin can interact with a resource from another origin. It helps isolate potentially malicious documents, reducing possible attack vectors.

  Two URLs have the same origin if the protocol, port (if specified), and host are the same for both. You may see this referenced as the "scheme/host/port tuple", or just "tuple". (A "tuple" is a set of items that together comprise a whole — a generic form for double/triple/quadruple/quintuple/etc.)

  ***

- Why is it called a Ternary operator, what does the word "Ternary" indicate?

  ***

  The ternary operator is a form of syntactic sugar for if-then-else statements. It is also known as the conditional operator, which is perhaps a more meaningful name because it evaluates conditions like if does.

  The name ternary refers to the fact that the operator takes three operands.

  ***

- What is strict mode? What are some of the advantages/disadvantages of using it?

  ***

  ```javascript
  (function () {
    "use strict"; // this is important
    function doSomething() {
      // this runs in strict mode
    }
    function doSomethingElse() {
      // so does this
    }
  })();
  ```

  pros:

  1. Eliminate some unreasonable and imprecise aspects of Javascript syntax and reduce some weird behaviors;

  2. Eliminate some insecure parts of the code to ensure the security of the code;

  3. Improve compiler efficiency and increase running speed;

  4. Pave the way for a new version of Javascript in the future.

  Disadvantages:

  Now the JS of the site will be compressed, some files use strict mode, while others do not. At this time, these files, which were originally strict patterns, were merged, and the string reached the middle of the file. Not only did it not indicate strict mode, but it wasted bytes after compression.

  ***

- What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?

  ***

  Some examples of languages that compile to JavaScript include CoffeeScript, Elm, ClojureScript, PureScript, and TypeScript.

  Advantages:

  1. Fixs some of the longstand problems in JavaScript and discourage JavaScript anti-patterns. E.g. Referring to the non-existent undefined constant

  2. Provides some syntatic sugar on top of JavaScript. Especially before ES6

  3. Static types are awesome (in the case of TypeScript) for large projects that need to be maintained over time.

  Disadvantage:

  1. Require a build/compile process as browsers only run javascript. The project needs to compile the code to into js first before being served to browser.

  2. Debugging can be a pain if your source maps do not map nicely to your pre-compiled source.

  3. Most developers are not familiar with these languages and will need to learn it. There's a ramp up cost involved for your team if you use it for your projects.

  ***

- What tools and techniques do you use debugging JavaScript code?

  ***

  Browser development tool.
  Add console.log, add debugger..., step execustion.

  React Devtools

  Redux Devtool

  ***

- Explain the difference between mutable and immutable objects.

  ***

  Immutability is a core principle in functional programming, and has lots to offer to object-oriented programs as well. A mutable object is an object whose state can be modified after it is created. An immutable object is an object whose state cannot be modified after it is created.

  ***

  - What is an example of an immutable object in JavaScript?

    ***

    In JavaScript, some built-in types (numbers, strings) are immutable, but custom objects are generally mutable.

    Some built-in immutable JavaScript objects are Math, Date.

    ***

  - What are the pros and cons of immutability?

    ***

    pros:

    1. Easier change detection: reference change.
    2. Less complicated to think about, don't need to worry how ojects evolve over time.
    3. Defensive copies are no longer necessary when immutable object are returning from or passed to functions, since immutable object will not be modified by it.
    4. Just pass the reference

    cons:

    1. Bad implementation occupied much memory
    2. Allocation (and deallocation) of many small objects rather than modifying existing ones can cause a performance impact. The complexity of either the allocator or the garbage collector usually depends on the number of objects on the heap.

    ***

  - How can you achieve immutability in your own code?

    ***

    1. use libraries like immutatble.js.

    2. Object Constant Properties: make writable to false and configurable: false. cannot be changed, redefined or deleted

       ```javascript
       let myObject = {};
       Object.defineProperty(myObject, "number", {
         value: 42,
         writable: false,
         configurable: false,
       });
       console.log(myObject.number); // 42
       myObject.number = 43;
       console.log(myObject.number); // 42
       ```

    3. Prevent Extensions, prevent add new property

       ```javascript
       var myObject = {
         a: 2,
       };

       Object.preventExtensions(myObject);

       myObject.b = 3;
       myObject.b; // undefined
       ```

    4. Seal

       Object.seal() creates a "sealed" object, which means it takes an existing object and essentially calls Object.preventExtensions() on it, but also marks all its existing properties as configurable: false.

       So, not only can you not add any more properties, but you also cannot reconfigure or delete any existing properties (though you can still modify their values).

    5. Freeze

       Object.freeze() creates a frozen object, which means it takes an existing object and essentially calls Object.seal() on it, but it also marks all "data accessor" properties as writable:false, so that their values cannot be changed.

       This approach is the highest level of immutability that you can attain for an object itself, as it prevents any changes to the object or to any of its direct properties (though, as mentioned above, the contents of any referenced other objects are unaffected).

    ***

- Explain the difference between synchronous and asynchronous functions.

  ***

  Synchronous functions are blocking while asynchronous functions are not. In synchronous functions, statements complete before the next statement is run. In this case, the program is evaluated exactly in order of the statements and execution of the program is paused if one of the statements take a very long time.

  Asynchronous functions usually accept a callback as a parameter and execution continue on the next line immediately after the asynchronous function is invoked. The callback is only invoked when the asynchronous operation is complete and the call stack is empty. Heavy duty operations such as loading data from a web server or querying a database should be done asynchronously so that the main thread can continue executing other operations instead of blocking until that long operation to complete (in the case of browsers, the UI will freeze).

  ***

- What is event loop?
  ***
  ***
  - What is the difference between call stack and task queue?
- What are the differences between variables created using `let`, `var` or `const`?

  ***

  JavaScript language is single-threaded and the asynchronous behaviour is not part of the JavaScript language itself, rather they are built on top of the core JavaScript language in the browser (or the programming environment) and accessed through the browser APIs.

  Answer:

  1. Not only need call stack to arrange the order but also need task queues to handle callback functions.

     **Task queues** can be divided to two types: macro-task and micro-task

     macro-tasks:
     |Browser|Node|
     |----|----|
     |script|script|
     |setTimeOut|setTimeOut|
     |setImmediate|setImmediate|
     |setInterval|setInterval|
     |I/O|I/O|
     |UI Render||

     micro-tasks:
     |Browser|Node|
     |----|----|
     |process.nextTick|process.nextTick|
     |Promise|new Promise().then|
     |Async/Await|setImmediate|
     |MutationObserver|setInterval|

  2. Drawer diagram

     Browser:
     !! **When callstack is empty**, then excute micro tasks, then execute macro task, then execute micro-tasks from this marco task. if any new micro-tasks generated
     ![image](https://cdn.javascripttutorial.net/wp-content/uploads/2019/12/javascript-event-loop.png)

     Node:  
      ┌───────────────────────────┐
     ┌─>│ timers │
     │ └─────────────┬─────────────┘
     │ ┌─────────────┴─────────────┐
     │ │ pending callbacks │
     │ └─────────────┬─────────────┘
     │ ┌─────────────┴─────────────┐
     │ │ idle, prepare │
     │ └─────────────┬─────────────┘ ┌───────────────┐
     │ ┌─────────────┴─────────────┐ │ incoming: │
     │ │ poll │<─────┤ connections, │
     │ └─────────────┬─────────────┘ │ data, etc. │
     │ ┌─────────────┴─────────────┐ └───────────────┘
     │ │ check │
     │ └─────────────┬─────────────┘
     │ ┌─────────────┴─────────────┐
     └──┤ close callbacks │
     └───────────────────────────┘

     (incoming data)->(poll)->(check)->(close callback)->(timers)->I/O (I/O callbacks)->(idle, prepare)->..

  3. Await/async order (chrome V8 engine):

     1. If await next is a variable(sync), wrapper it to a micro task like `.then` to queue. (What V8 engine has now, it is anti-pattern. Before it will be put to the end of queue, kind like the second point).
     2. If await next is a async, after registering the async, it jump out of await function and continue. when callstack is empty, then it will go back to code follow by array.

  4. Node 11 change

     Node 11, it is like browser, one macro task, (next tick is normal microtask now)then its microtasks...

     Before node 11, eveey loop phase will check setImmediate queue, if there is any one, excute it before micro-tasks, then `.nextTick()`, then micro-tasks.

  for more: https://cloud.tencent.com/developer/article/1601176 (CN)

  ***

- What are the differences between ES6 class and ES5 function constructors?

  ***

  | ES6 class                                                 | ES5 function constructors                                                                                                                    |
  | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
  | Define a new object and append functions to its prototype | Function constructors looks the same, but needs `prototype` key word to append functions later. (Inheritence also needs to assign prototype) |
  | Ensure this key word is used inside                       | ES5 function constructor focus on implementing the reusable object creation code. Any function can be used as a constructor.                 |
  | Are not hoisted                                           | Hoisted                                                                                                                                      |
  | Static key word                                           |                                                                                                                                              |
  | use strict by default                                     |                                                                                                                                              |

  \*class can extend function constructor

  ***

- Can you offer a use case for the new arrow `=>` function syntax? How does this new syntax differ from other functions?

  ***

  setTimeout callback use arrow, use arrow function is closed over enclosing scope, it can access this over onside setTimeout. function declaration can not do this.
  // ES6

  ```javascript
  var obj = {
    id: 42,
    counter: function counter() {
      setTimeout(() => {
        console.log(this.id);
      }, 1000);
    },
  };
  ```

  ***

- What advantage is there for using the arrow syntax for a method in a constructor?

  ***

  _That the value of this gets set at the time of the function creation and can't change after that._ So, when the constructor is used to create a new object, this will always refer to that object.

  The main takeaway here is that this can be changed for a normal function, but the context always stays the same for an arrow function. So even if you are passing around your arrow function to different parts of your application, you wouldn't have to worry about the context changing.

  ***

- What is the definition of a higher-order function?

  ***

  The main takeaway here is that this can be changed for a normal function, but the context always stays the same for an arrow function. So even if you are passing around your arrow function to different parts of your application, you wouldn't have to worry about the context changing.

  Examples are Array methods like Array.prototype.map, Array.prototype.filter

  ***

- Can you give an example for destructuring an object or an array?

  ***

  ```javascript
  const obj = {
    key1: "1",
    key2: "2",
  };

  const { key1, key2: newKey2 } = obj;

  const arr = [1, 2];
  const [first, second] = arr;
  ```

  ***

- Can you give an example of generating a string with ES6 Template Literals?
  ```javascript
  const variable = "aaa";
  console.log(`${aaa}`);
  ```
- Can you give an example of a curry function and why this syntax offers an advantage?

  ***

  Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).

  This technique can be useful for making code written in a functional style easier to read and compose.

  Higher oder function is React is an example of curry

  ***

- What are the benefits of using `spread syntax` and how is it different from `rest syntax`?

  ***

  spread syntax: can be used in object and array.

  ```javascript
  const newAnimalsArray = [ …domesticAnimals, …notSoDomesticAnimals];
  ```

  rest syntax: get remaining element inside an array.
  const newAnimalsArray = [ …domesticAnimals, …notSoDomesticAnimals];

  ```javascript
  const notSoDomesticAnimals = ['Salamander', 'Iguana', 'Moth', 'Sloth'];
  const [salamander, iguana, …rest] = notSoDomesticAnimals;
  ```

  the difference between the rest and spread syntax is that while spread copies everything, rest is used when we want to retrieve all remaining elements (or all existing elements) after a destructuring operation.

  ***

- How can you share code between files?

  ***

  This depends on the JavaScript environment.

  On the client (browser environment), as long as the variables/functions are declared in the global scope (window), all scripts can refer to them. Alternatively, adopt the Asynchronous Module Definition (AMD) via RequireJS for a more modular approach.

  On the server (Node.js), the common way has been to use CommonJS. Each file is treated as a module and it can export variables and functions by attaching them to the module.exports object.

  ES2015 defines a module syntax which aims to replace both AMD and CommonJS. This will eventually be supported in both browser and Node environments.

  ***

- Why you might want to create static class members?
  ***
  Static class members (properties/methods) are not tied to a specific instance of a class and have the same value regardless of which instance is referring to it. Static properties are typically configuration variables and static methods are usually pure utility functions which do not depend on the state of the instance.
  ***
- What is the difference between `while` and `do-while` loops in JavaScript?

  ***

  while: check the condition first.

  do-while: execute the loop once then check the condition to decide whether go back to the loop.

  ***

- What is a promise? Where and how would you use promise?

  ***

  A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future.

  whenever you will use async function

  ***

## Coding questions

- Make this work:

```javascript
duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]

return [...array, ...array];
```

- Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`

  ```javascript
  for (let i = 3; i <= 100; i++) {
    if (i % 3 === 0) {
      console.log("fizz");
      if (i % 5 === 0) {
        console.log("fizzbuzz");
      }
    } else if (i % 5 == 0) {
      console.log("buzz");
    }
  }
  ```

- What will be returned by each of these?

```javascript
console.log("hello" || "world"); // hello
console.log("foo" && "bar"); // bar
```

- Write an immediately invoked function expression (IIFE)

```javascript
(function () {
  console.log("IIFC");
})();
```

Note:

arrow function scope is fixed is where it is created.
