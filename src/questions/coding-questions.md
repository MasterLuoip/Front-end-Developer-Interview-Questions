---
title: Coding Questions
layout: layouts/page.njk
permalink: /questions/coding-questions/index.html
---

Question: What is the value of `foo`?

```javascript
var foo = 10 + "20"; // 1020
```

Question: What will be the output of the code below?

```javascript
console.log(0.1 + 0.2 == 0.3); // false
```

---

Because number in JS is represented in floating point 64 bit. It has round issue. For more: https://stackoverflow.com/questions/25925284/javascript-floating-point-number-confusion

---

Question: How would you make this work?

```javascript
add(2, 5); // 7
add(2)(5); // 7

function add(first, second) {
  if (arguments.length < add.length) {
    return function y(second) {
      return first + second;
    };
  } else {
    return first + second;
  }
}
```

Question: What value is returned from the following statement?

```javascript
"i'm a lasagna hog".split("").reverse().join("");
//"goh angasal a m'i"
```

Question: What is the value of `window.foo`?

```javascript
window.foo || (window.foo = "bar");
// bar this is normal initial
```

Question: What is the outcome of the two alerts below?

```javascript
var foo = "Hello"; // global scope
(function () {
  var bar = " World"; // function scope
  alert(foo + bar); // Hello World
})();
alert(foo + bar); // bar is undefined
```

Question: What is the value of `foo.length`?

```javascript
var foo = [];
foo.push(1);
foo.push(2);
// 2
```

Question: What is the value of `foo.x`?

```javascript
var foo = { n: 1 };
var bar = foo;
foo.x = foo = { n: 2 };

// undefined
/*
determines that foo.x refers to a property x of the {n: 1} object, assigns {n: 2} to foo, and assigns the new value of foo – {n: 2} – to the property x of the {n: 1} object.

The important thing is that the foo that foo.x refers to is determined before foo changes.
*/
```

Question: What does the following code print?

```javascript
console.log("one");
setTimeout(function () {
  console.log("two");
}, 0);
Promise.resolve().then(function () {
  console.log("three");
});
console.log("four");
// one four three two
```

Question: What is the difference between these four promises?

```javascript
// return doSomethingElse() call result
// Chained in Sequence, with no parameter passing.
doSomething().then(function () {
  return doSomethingElse();
});

// do nothing, return nothing
// Executed in Sequence (not chained), with no parameter passing.
doSomething().then(function () {
  doSomethingElse();
});

// call function
// This is pretty much never what you want. This executes doSomething() and then, before doSomething() has resolved, it also executes doSomethingElse() and passes the return value from doSomethingElse() as the .then() handler. This is a coding mistake unless doSomethingElse() returns a function to be used as the .then() handler.
// Executed Immediately, Probably a Bug
doSomething().then(doSomethingElse());

// return function name
// This is the same as option 1 except that the resolved value from doSomething() is passed as the first argument to doSomethingElse(val). This is structurally the same as this:
// Chained in Sequence, with parameter passing.
doSomething().then(doSomethingElse);
```

for more: https://stackoverflow.com/questions/49592105/javascript-es6-promises

Question: What will the code below output to the console and why?

```javascript
(function () {
  var a = (b = 3);
  // no working in strict mode
  // equals to
  // b = 3;
  // var a = b;
  // b ends up being a global variable
})();

console.log("a defined? " + (typeof a !== "undefined"));
// false
console.log("b defined? " + (typeof b !== "undefined"));
// true
```

Question: Consider the two functions below. Will they both return the same thing? Why or why not?

```javascript
function foo1() {
  return {
    bar: "hello",
  };
}

function foo2() {
  return;
  console.log(123);
  {
    bar: "hello";
  }
}
/*
foo1 returns:
Object {bar: "hello"}
foo2 returns:
undefined
*/
```

The reason for this has to do with the fact that semicolons are technically optional in JavaScript (although omitting them is generally really bad form). As a result, when the line containing the return statement (with nothing else on the line) is encountered in foo2(), a semicolon is automatically inserted immediately after the return statement.

No error is thrown since the remainder of the code is perfectly valid, even though it doesn’t ever get invoked or do anything (it is simply an unused code block that defines a property bar which is equal to the string "hello").
