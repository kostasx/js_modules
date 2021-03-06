---
title: "JavaScript Module 2"
author: "Social Hackers Code School"
created: "Sun Oct 29 2017 18:04:15 GMT+0200 (EET)"
original:
    title: "JavaScript Module 2"
    url: "file:///Users/Pouianou/projects/kajero-notebooks/social_hackers/js_week_2/functions.html"
show_footer: false
---

## Functions

#### 1. Definition and declaration
- A function is a block of code stored as a value. The type of this value is "function".
- A function can be defined as any other variable, through what we call a _function expression_, or through a _function declaration_:

```javascript; runnable
// Function declaration
function hi() {
  console.log('Hi');
}

// Function expression
var hello = function () {
  console.log('Hello');
}
```

#### 2. Execution and the _return_ statement
- Functions are _executed_ when _called_:

```javascript; runnable
var greet = function () {
  console.log('Hello');
}

greet();
```

- All functions have a return value, which defaults to _undefined_:

```javascript; runnable
function getName () {
  return 'James';
}

function greet() {
  console.log('Hi, ');
}

const name = getName();

greet();
console.log(name);
```

#### 3. Parameters and aguments
- Functions can be _passed_ values as _arguments_ through _parameters_ declared by the function.

```javascript; runnable
// a, b are function parameters
function add(a, b) {
  return a + b;
}

// 'add' is called with arguments 1, 2
var three = add(1, 2);

console.log(three);
```

- Functions can have any number of _parameters_. In JS, we can also pass any number of _arguments_ to a function:

```javascript; runnable
function greet(greeting, name, surname) {
  console.log(greeting + ' ' + name + ' ' + surname + '!');
}

greet('Hello', 'James', 'Bond');

// Fewer arguments than parameters
greet('Hi', 'James');

// More arguments than parameters
greet('Hello', 'there', 'Mr.', 'Bond');

// Order matters!
greet('Bond', 'James', 'Hi');
```

- Functions can define _default values_ for their parameters:

```javascript; runnable
function greetUser(userName) {
  let name = 'James';

  if (userName) {
    name = userName;
  }

  console.log(`Hello, ${name}`);
}

greetUser('Maria');
greetUser();
```

```javascript; runnable
const user = {
  name: 'Jim',
  surname: 'Morisson'
}

function getUserName(user) {
  return user.name;
}

function greetByName(user) {
  const name = getUserName(user);
  console.log(`Hello, ${name}`);
}

greetByName(user);
greetByName({ name: 'Maria' });
greetByName();
```

- Any value type can be passed as an argument, including other functions!

```javascript; runnable
function reduce (numbers) {
  let sum = 0;

  for(var i = 0; i < numbers.length; i++) {
      sum += numbers[i];
  }

  return sum;
}

console.log(reduce([1, 2, 3, 4]));
```

```javascript; runnable
function addNumbers(a, b) {
  return a + b;
}

function plusOne(num, add) {
  return add(num, 1);
}

console.log(plusOne(3, addNumbers));
```

#### 4. Scope

- Think of scope as an "area" where some variables are "active", or, more simply, "exist". There are more types of scope: local, and global. Local scope has various 'degrees of localness'.
- All functions have access to _global_ variables.
- _Parameters_ and variables _declared_ inside a function are _local_ to that function.
- Each local scope can also see all the local scopes that contain it

```javascript; runnable
// a is a global variable
const a = 1;

function plusOne(num) {
  return num + a;
}

console.log(plusOne(3));
```

```javascript; runnable
// 'one' is a local variable
function plusOne(num) {
  const one = 1;
  return num + one;
}

function plusTwo(num) {
  return num + one + one;
}

console.log(plusOne(1));
console.log(plusTwo(1));
```

```javascript; runnable
// Function scope - the inner function has access to
// variables declared on the parent function
function reduce(numbers) {
  let sum = 0;

  function increaseSum(num) {
    return sum + num;
  }

  for (let i = 0; i < numbers.length; i++) {
    sum = increaseSum(numbers[i]);
  }

  return sum;
}

const sum = reduce([1, 2, 3]);
console.log(`The sum is ${sum}`);

const increasedSum = increaseSum(1);
console.log(increasedSum);
```
