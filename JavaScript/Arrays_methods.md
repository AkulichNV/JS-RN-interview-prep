# JavaScript Array Methods Cheat Sheet

Arrays are fundamental data structures in JavaScript, offering a suite of built-in methods to manipulate and traverse data efficiently. 
Below is a cheat sheet for 20 of the most commonly used array methods, starting with the most versatile.

## 1. map()

Creates a new array populated with the results of calling a provided function on every element.

```javascript
const numbers = [1, 2, 3];
const squares = numbers.map(num => num * num);
// squares = [1, 4, 9]

```

## 2. forEach()

Executes a provided function once for each array element.

```javascript
const numbers = [1, 2, 3];
numbers.forEach(num => console.log(num));
// Output: 1 2 3
```

## 3. filter()

Creates a new array with all elements that pass the test implemented by the provided function.

```javascript
const newArray = array.filter(function(element, index, array) {
  // Return true to keep the element
});

const numbers = [1, 2, 3, 4];
const evens = numbers.filter(num => num % 2 === 0);
// evens = [2, 4]
```

## 4. reduce()

Executes a reducer function on each element of the array, resulting in a single output value.

```javascript
const result = array.reduce(function(accumulator, element, index, array) {
  // Return updated accumulator
}, initialValue);

const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, num) => acc + num, 0);
// sum = 10
```

## 5. find()

Returns the value of the first element in the array that satisfies the provided testing function.

```javascript
const foundElement = array.find(function(element, index, array) {
  // Return true when the element is found
});

const numbers = [1, 2, 3, 4];
const firstEven = numbers.find(num => num % 2 === 0);
// firstEven = 2
```

## 6. findIndex()

Returns the index of the first element in the array that satisfies the provided testing function.

```javascript
const index = array.findIndex(function(element, index, array) {
  // Return true when the element is found
});

const numbers = [1, 2, 3, 4];
const indexOfFirstEven = numbers.findIndex(num => num % 2 === 0);
// indexOfFirstEven = 1
```

## 7. includes()

Determines whether an array includes a certain value.

```javascript
const exists = array.includes(valueToFind, fromIndex);

const fruits = ['apple', 'banana', 'mango'];
const hasMango = fruits.includes('mango');
// hasMango = true
```

## 8. some()

Tests whether at least one element in the array passes the test implemented by the provided function.

```javascript
const result = array.some(function(element, index, array) {
  // Return true if condition is met
});

const numbers = [1, 3, 5];
const hasEven = numbers.some(num => num % 2 === 0);
// hasEven = false
```

## 9. every()

Tests whether all elements in the array pass the test implemented by the provided function.

```javascript
const result = array.every(function(element, index, array) {
  // Return true if condition is met for all elements
});

const numbers = [2, 4, 6];
const allEven = numbers.every(num => num % 2 === 0);
// allEven = true
```

## 10. push()

Adds one or more elements to the end of an array and returns the new length of the array.

```javascript
const numbers = [1, 2];
numbers.push(3, 4);
// numbers = [1, 2, 3, 4]
```

## 11. pop()

Removes the last element from an array and returns that element.

```javascript
const numbers = [1, 2, 3];
const last = numbers.pop();
// last = 3, numbers = [1, 2]
```

## 12. shift()

Removes the first element from an array and returns that element.

```javascript
const numbers = [1, 2, 3];
const first = numbers.shift();
// first = 1, numbers = [2, 3]
```

## 13. unshift()
Adds one or more elements to the beginning of an array and returns the new length of the array.

```javascript
const numbers = [3, 4];
numbers.unshift(1, 2);
// numbers = [1, 2, 3, 4]
```

## 14. slice()

Returns a shallow copy of a portion of an array into a new array object.

```javascript
const newArray = array.slice(beginIndex, endIndex);

const numbers = [1, 2, 3, 4, 5];
const sliced = numbers.slice(1, 4);
// sliced = [2, 3, 4]
```

## 15. splice()

Changes the contents of an array by removing or replacing existing elements and/or adding new elements.

Syntax:

```javascript
const removedElements = array.splice(startIndex, deleteCount, item1, item2, ..., itemN);

const numbers = [1, 2, 5, 6];
numbers.splice(2, 0, 3, 4);
// numbers = [1, 2, 3, 4, 5, 6]
```

## 16. concat()

Merges two or more arrays and returns a new array.

```javascript
const newArray = array1.concat(array2, array3, ..., arrayN);

const a = [1, 2];
const b = [3, 4];
const c = a.concat(b);
// c = [1, 2, 3, 4]
```

## 17. indexOf()

Returns the first index at which a given element can be found in the array, or -1 if it is not present.

```javascript
const index = array.indexOf(searchElement, fromIndex);

const fruits = ['apple', 'banana', 'mango'];
const index = fruits.indexOf('banana');
// index = 1
```

## 18. join()

Joins all elements of an array into a string.

```javascript
const string = array.join(separator);

const fruits = ['apple', 'banana', 'mango'];
const fruitString = fruits.join(', ');
// fruitString = 'apple, banana, mango'
```

## 19. reverse()

Reverses an array in place.

```javascript
const numbers = [1, 2, 3];
numbers.reverse();
// numbers = [3, 2, 1]
```

## 20. sort()

Sorts the elements of an array in place and returns the sorted array.

```javascript
array.sort([compareFunction]);

const numbers = [3, 1, 4, 2];
numbers.sort();
// Default sort (lexicographical): [1, 2, 3, 4]

// Numeric sort
numbers.sort((a, b) => a - b);
// numbers = [1, 2, 3, 4]
```
