## Temporal Dead Zone (TDZ)

### Overview:
* The Temporal Dead Zone (TDZ) refers to the time period during which a `let`, `const`, or `class` declaration is in scope but not yet initialized.
* Accessing the variable during this period results in a ReferenceError.

### Key Points:
#### 1. TDZ for `let`:
* Variables declared with let and const are hoisted to the top of their block, but are not initialized.
* The TDZ starts from the beginning of the block until the variable is initialized.
```javascript
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;
```

#### 2. No TDZ for `var`:
* Variables declared with `var` are also hoisted but initialized with undefined.
* Accessing them before the declaration does not result in a `ReferenceError`.
```javascript
console.log(b); // undefined
var b = 10;
```

#### 3. TDZ in `const`:
* Variables declared with `const` must be initialized at the time of declaration.
* The TDZ behaves similarly to `let`, but any attempt to use the variable before initialization or without initialization results in an error.
```javascript
console.log(c); // ReferenceError: Cannot access 'c' before initialization
const c = 20;
```

#### 4. TDZ in `class`:
* Classes declared using the `class` keyword are also subject to the TDZ.
* You cannot reference a class before it is fully declared.
```javascript
const instance = new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization
class MyClass {}
```

### Key Scenarios:
#### 1. Function Scope vs Block Scope:
* `let` and `const` are block-scoped, meaning their TDZ applies within the closest enclosing block (e.g., `{}`, `if`, `for` loops).
* `var` is function-scoped and not subject to TDZ.
```javascript
function example() {
    console.log(x); // ReferenceError
    if (true) {
        let x = 10;
    }
}
```

#### 2. TDZ and Default Parameters:
* The TDZ also applies to variables used as default values in function parameters.
```javascript
function example(y = x) { // ReferenceError
    let x = 2;
    return y;
}
example();
```

#### 3. TDZ and Loops:
* Variables declared with `let` inside a loop are also hoisted to the top of the block, and their TDZ starts from the beginning of the block.
```javascript
for (let i = 0; i < 5; i++) {
    console.log(i); // Works fine
}
console.log(i); // ReferenceError: i is not defined
```

## Summary:
* The TDZ ensures that variables are not accessed before they are declared and initialized.
* It enforces cleaner and more predictable code by avoiding the use of uninitialized variables.
* Understanding TDZ helps prevent `ReferenceError` in JavaScript and promotes better coding practices.
