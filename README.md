# Advanced JavaScript Concepts (Quick Guide)

A concise guide to important advanced JavaScript concepts with short explanations and code examples.


1\. **Event Loop**
------------------

The event loop allows JavaScript to perform non-blocking operations by offloading operations to the browser and queuing a callback.

```
console.log('Start');

setTimeout(() => {
  console.log('Callback');
}, 0);

console.log('End');
// Output:
// Start
// End
// Callback

```


2\. **Call Stack**
------------------

JavaScript uses a call stack to manage function execution. Last-in, first-out (LIFO) structure.

```
function first() {
  second();
}

function second() {
  console.log('Second function');
}

first();
// Call stack: first() → second()

```


3\. **Event Delegation**
------------------------

Instead of attaching listeners to multiple child elements, use one on a parent.

```
<ul id="parent">
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

```

```
document.getElementById('parent').addEventListener('click', (e) => {
  if (e.target.tagName === 'LI') {
    console.log(e.target.textContent);
  }
});

```


4\. **Closures**
----------------

A closure is a function that remembers variables from its outer scope.

```
function outer() {
  let count = 0;
  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2

```


5\. **Hoisting**
----------------

Variable and function declarations are moved to the top of their scope during compilation.

```
console.log(a); // undefined
var a = 5;

```

```
hoisted(); // Works

function hoisted() {
  console.log('Hoisted!');
}

```


6\. **Promises**
----------------

Used for asynchronous operations. Promises have `resolve` and `reject`.

```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done!"), 1000);
});

myPromise.then(console.log); // Done!

```


7\. **Async/Await**
-------------------

Syntactic sugar over promises for better readability.

```
async function fetchData() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  console.log(data);
}

```


8\. **Debounce & Throttle**
---------------------------

Used to control function execution frequency.

**Debounce:** Runs after a pause in events.

```
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

```

**Throttle:** Runs at most once every interval.

```
function throttle(fn, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}

```


9\. **Currying**
----------------

Breaking a function into multiple functions that take one argument.

```
function add(a) {
  return function (b) {
    return a + b;
  };
}

console.log(add(2)(3)); // 5

```


10\. **Prototype & Prototypal Inheritance**
-------------------------------------------

JavaScript uses prototypes for inheritance.

```
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log('Hi, I am ' + this.name);
};

const p = new Person('Alice');
p.sayHello(); // Hi, I am Alice

```


11\. **this Keyword**
---------------------

Refers to different things based on how a function is called.

```
const person = {
  name: 'John',
  greet() {
    console.log('Hi, ' + this.name);
  }
};

person.greet(); // Hi, John

```


12\. **IIFE (Immediately Invoked Function Expression)**
-------------------------------------------------------

Runs as soon as it's defined.

```
(function () {
  console.log('IIFE runs immediately!');
})();

```


13\. **Modules (ES6)**
----------------------

Used to organize code into reusable files.

```
// math.js
export function add(a, b) {
  return a + b;
}

// main.js
import { add } from './math.js';
console.log(add(2, 3));

```


14\. **Garbage Collection**
---------------------------

Automatic memory management -- unused variables are cleaned up when unreachable.

```
let a = { name: 'test' };
a = null; // 'test' is now eligible for garbage collection

```


15\. **WeakMap / WeakSet**
--------------------------

Collections that hold "weak" references. Keys must be objects.

```
let obj = {};
let wm = new WeakMap();
wm.set(obj, 'value');

obj = null; // Garbage collected

```
