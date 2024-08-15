## 1. Understanding Context and Lexical Environments

* **Context:** Refers to the value of `this` within a function. It is determined by how the function is called (e.g., object method, global function, constructor function).
* **Lexical Environment:** Refers to the scope within which variables are defined. It is created every time a function is invoked, comprising:
   * **Environment Record:** Stores local variables, parameters, and inner function declarations.
   * **Outer Lexical Environment Reference:** Points to the lexical environment of the parent context, allowing access to variables outside the current function.
```javascript
function outer() {
    let outerVar = 'I am outside!';
    function inner() {
        let innerVar = 'I am inside!';
        console.log(outerVar); // Accessing variable from outer lexical environment
    }
    inner();
}
outer();
```

## 2. Differences Between Scope and Context

### Scope:
* Deals with the accessibility of variables.
* **Global Scope:** Variables accessible from anywhere in the code.
* **Function Scope:** Variables accessible within the function they are declared.
* **Block Scope (ES6):** Variables defined within a block `{}` using `let` or `const`.
```javascript
let globalVar = "I'm global";
function scopeExample() {
    let functionVar = "I'm in a function";
    if (true) {
        let blockVar = "I'm in a block";
        console.log(blockVar); // Accessible here
    }
    console.log(functionVar); // Accessible here
    console.log(globalVar); // Accessible here
}
```

### Context:
* Refers to the value of `this`.
* **Global Context:** `this` refers to the global object (`window` in browsers).
* **Function Context:** `this` refers to the object calling the function.
```javascript
const obj = {
    name: "Object",
    logThis: function() {
        console.log(this); // Refers to obj
    }
};
obj.logThis(); // obj context
```

## 3. The Mechanism of Lexical Environment Traversal

* When a variable is accessed, JavaScript first looks in the current lexical environment. If not found, it traverses up the lexical environment chain to the parent context, continuing until the global environment.
```javascript
function outer() {
    let outerVar = 'Outer';
    function inner() {
        let innerVar = 'Inner';
        console.log(outerVar); // Lexical environment traversal to find outerVar
    }
    inner();
}
outer();
```

* If a variable is not found after traversing all environments, a `ReferenceError` is thrown.

## 4. Connection Between Function and Its Lexical Environment

* Every function "remembers" the lexical environment where it was created. This is the essence of closures.
```javascript
function createCounter() {
    let count = 0;
    return function increment() {
        count++;
        console.log(count);
    };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
```

* Here, `increment` is a closure. It captures the lexical environment of `createCounter` and continues to access `count` even after `createCounter` has finished executing.
* **Closure:** A function combined with its lexical environment. It allows the function to access variables from its scope even after the outer function has closed.
```javascript
function outerFunction(outerVariable) {
    return function innerFunction(innerVariable) {
        console.log(`Outer: ${outerVariable}`);
        console.log(`Inner: ${innerVariable}`);
    };
}

const newFunction = outerFunction('outside');
newFunction('inside');
```
* In this example, `innerFunction` has closed over `outerFunction`'s lexical environment and can access `outerVariable`.

## Summary
* **Context** (`this`) is dynamic and depends on how a function is called.
* **Lexical Environment** is static and determined by where the function was declared.
* **Scope** is about visibility/accessibility of variables.
* **Closure** connects a function to its lexical environment, allowing access to outer scope variables after the outer function has completed execution.
* 
