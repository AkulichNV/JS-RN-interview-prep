### 1. `call` Method

* **Purpose:** Invokes a function and allows you to specify the `this` context and arguments.
* **Syntax:** `func.call(thisArg, arg1, arg2, ...)`
* **Example:**
```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Alice' };

greet.call(person, 'Hello', '!'); // Output: "Hello, Alice!"
```

### 2. `apply` Method

* **Purpose:** Invokes a function and allows you to specify the `this` context and an array of arguments.
* **Syntax:** `func.apply(thisArg, [argsArray])`
* **Example:**
```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Bob' };

greet.apply(person, ['Hi', '?']); // Output: "Hi, Bob?"
```
* **Difference from `call`:** `apply` takes an array of arguments instead of individual arguments.

### 3. `bind` Method

* **Purpose:** Creates a new function that, when called, has its `this` context set to the provided value, with a given sequence of arguments preceding any provided when the new function is invoked.
* **Syntax:** `const boundFunc = func.bind(thisArg, arg1, arg2, ...)`
* **Example:**
```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Charlie' };

const greetPerson = greet.bind(person, 'Hey');

greetPerson('!!!'); // Output: "Hey, Charlie!!!"
```
* **Usage Note:** `bind` does not invoke the function immediately; it returns a new function that can be called later.

### 4. Comparison Summary

* **`call`:** Immediately invokes the function with the specified `this` value and arguments.
* **`apply`:** Immediately invokes the function with the specified `this` value and an array of arguments.
* **`bind`:** Returns a new function with a specific `this` value and optionally, preset arguments.

### 5. Practical Use Cases

* **`call`:** Useful when you need to call a function with a specific `this` context and individual arguments.
* **`apply`:** Ideal when dealing with functions like `Math.max` that can take multiple arguments in an array.
```javascript
const numbers = [5, 6, 2, 3, 7];
const max = Math.max.apply(null, numbers); // Output: 7
```
* **`bind`:** Useful when you need a function to always be called with a specific `this` value, like in event handlers.
```javascript
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
};

const retrieveX = module.getX;
console.log(retrieveX()); // Output: undefined, because `this` is not bound

const boundGetX = module.getX.bind(module);
console.log(boundGetX()); // Output: 42
```
