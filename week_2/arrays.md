---
title: "JS Module 2 - Arrays"
author: "Social Hackers Code School"
created: "Sun Oct 29 2017 17:57:36 GMT+0200 (EET)"
original:
    title: "JS Module 2 - Arrays"
    url: "file:///Users/Pouianou/projects/kajero-notebooks/social_hackers/js_week_2/arrays.html"
show_footer: false
---

## Arrays

#### 1. Definition
- Arrays are special objects used to store sequences of values.
- All arrays are instances of the global `Array` object.
- Arrays have `typeof === 'object'` and are `instanceof` Array
- Arrays can hold any type of value, including other arrays

```javascript; runnable
const fruit = ['apple', 'banana', 'orange'];

const numbers = [1, 2, 3];

const arrays = [fruit, numbers];

console.log(arrays);
```

#### 2. Array length

- Arrays can hold any number of elements. The number of elements in an array is called the array _length_. It is in fact a property on the Array object, and unlike the index, is 1-based.
- The Array.length property returns the nuber of element sin the array.

```javascript; runnable
const fruits = ['apple', 'banana', 'orange'];

console.log(`I have ${fruits.length} fruits`);
```

#### 3. Array index

- Arrays 'remember' the position of each element, and represent this position through a (0-based) number called _index_. The index can be used to directly refference array elements.
- The Array.indexOf(element) function returns the index of a given element.

```javascript; runnable
const fruits = ['apple', 'banana', 'orange'];

const first = fruits[0];

const last = fruits[length - 1];

const myFruit = fruits[1];


console.log(`The first fruit is ${first},\
the last fruit is ${last},\
but my favourite fruit is ${myFruit}.`);
```

#### 4. Adding elements with Array.push() and Array.unshift()

- Array.push() adds an element at the _end_ of the array.
- Array.unshift() adds an element at the start of the array.

```javascript; runnable
const fruits = ['apple', 'banana', 'orange'];

fruits.push('pear');
fruits.unshift('mango');

console.log(fruits);
```

#### 5. Removing elements with Array.pop() and Array.shift()

- Array.pop() removes the _last_ element from an array, and returns the element.
- Array.shift() removes the _first_ element from an array, and returns the element.

```javascript; runnable
const fruits = ['apple', 'banana', 'orange'];

console.log(`The first fruit is ${fruits[0]}.`);

const first = fruits.shift();

console.log(`Removed ${first}.\
 The first fruit is now ${fruits[0]}.`);


console.log(`The last fruit is ${fruits[fruits.length - 1]}.`);

const last = fruits.pop();

console.log(`Removed ${last}.\
 The last fruit is now ${fruits[fruits.length - 1]}.`);
```

#### 6. Removing all elements from an array

- Many ways to do this (can you think of some?)
- TL;DR - use Array.length = 0;

```javascript; runnable
const fruits = ['apple', 'banana', 'orange'];

fruits.length = 0;

console.log(fruits);
```

#### 7. Copying parts of an array with Array.slice()

- Array.slice(begin, end) will return a copy of a part of an array, starting from the element at the 'begin' index (inclusive), and up to the element at the 'end' index (exclusive).
- If no arguments are passed the function will return a shallow copy of the entire array.
- Array.slice() does not mutate the original array.

```javascript; runnable
const numbers = [1, 2, 3, 4, 5];

const lastTwo = numbers.slice(3);

const firstTwo = numbers.slice(0, 2);
console.log(`The first two numbers are ${firstTwo}. The last two numbers are ${lastTwo}.`);
```

```javascript; runnable
// Example of shallow copy
let fruits = ['apple', 'banana', 'orange'];

const copy1 = fruits;

const copy2 = fruits;

const copy3 = fruits.slice();

fruits = [];

console.log(copy1);
console.log(copy2);
console.log(copy3);
console.log(copy1 === copy2);
console.log(copy1 === copy3);
```

```javascript; runnable
// Example of deep vs shallow copy
let fruits = ['apple', 'banana', 'orange'];

let meats = ['chicken', 'lamb'];

let basket = [fruits, meats, 'milk'];

const copy = basket.slice();

basket[2] = 'eggs';
basket[1] = ['apple', 'banana'];

console.log(copy);
```

#### 8.1 Deleting parts of an array with Array.splice()

- Array.splice() can be used to delete entire parts of an array.
- Array.splice() takes two arguments, _begin_, and _count_.
- Array.plice() returns an array containing the removed elements.
- **Unlike Array.slice(), Array.splice() _mutates_ the original array!**

```javascript; runnable
const fruits = ['apple', 'banana', 'orange'];

function truncate(array, count) {
  return array.splice(array.length - count, count);
}

const lastTwo = truncate(fruits, 2);

console.log(lastTwo);
console.log(fruits);
```

#### 8.2 Adding and replacing elements with Array.splice()

- By passing elements as argument to Array.splice() after the _begin_ and _count_ arguments
- If we pass some elements as arguments, and the count argument is also === 0, then the provided element are simply added to the array.

```javascript; runnable
// Replacing an existing element with a new one
const fruits = ['apple', 'banana', 'orange'];

fruits.splice(1, 2, 'tangerine');

console.log(fruits);
```

```javascript; runnable
// Adding a new element to the array
const fruits = ['apple', 'banana', 'orange'];

fruits.splice(1, 0, 'tangerine');

console.log(fruits);
```

#### 9. Mapping arrays with Array.map()

- Array.map() returns a new array that holds all the values that are the result of executing a function passed as an argument, on the elements of the original (calling) array.
- Array.map() is super powerful and often used.


```javascript; runnable
// Example 9.1
const fruits = ['apple', 'banana', 'orange'];

function getIndices(array) {
  return array.map(function(element) {
    return array.indexOf(element);
  });
}

const indices = getIndices(fruits);

console.log(indices);
```

```javascript; runnable
// Example 9.2
const fruits = [
  {
    name: 'apple',
    color: 'red'
  },
  {
    name: 'banana',
    color: 'yellow'
  },
  {
    name: 'orange',
    color: 'orange'
  }
]

function getFruitColors(fruitCollection) {
  return fruitCollection.map(function (fruit) {
    return fruit.color;
  });
}

console.log(getFruitColors(fruits));
```

#### 10. String manipulation with Array.join() and String.split()

- Array.join(separator) returns a string containing all the elements in the array, joined by a separator passed as an _argument_. The separator _defaults_ to comma (',').
- String.split(separator) splits a string into multiple strings, based on a given separator. If no separator is passed as an argument, the original string is returned as is.
- Array.join() and String.split() do not have side effects.

```javascript; runnable
const phrase = 'Never gonna give you up';
const words = phrase.split(' ');
const commaPhrase = words.join(',');

console.log(phrase);
console.log(words);
console.log(commaPhrase);
```
