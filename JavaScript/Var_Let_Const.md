## `let`, `var`, and `const` 

### 1. `var`

#### Scope:
* Function-scoped.
* Accessible outside of block scope (e.g., inside if, for blocks).
#### Hoisting:
* Variables declared with var are hoisted to the top of their scope and initialized with undefined.
#### Re-declaration:
* Can be re-declared within the same scope.
#### Re-assignment:
* Can be reassigned to a new value.
```javascript
var x = 10;
if (true) {
    var x = 20;  // Same variable!
    console.log(x);  // 20
}
console.log(x);  // 20
```
*****

### 2. `let`

#### Scope:
* Block-scoped.
* Only accessible within the block it’s defined.
#### Hoisting:
* `let` is hoisted but not initialized. Accessing it before declaration results in a ReferenceError.
#### Re-declaration:
* Cannot be re-declared within the same scope.
#### Re-assignment:
* Can be reassigned to a new value.
```javascript
let y = 10;
if (true) {
    let y = 20;  // Different variable (block-scoped)
    console.log(y);  // 20
}
console.log(y);  // 10
```
*****

### 3. `const`

#### Scope:
* Block-scoped.
* Only accessible within the block it’s defined.
#### Hoisting:
* `const` is hoisted but not initialized. Accessing it before declaration results in a ReferenceError.
#### Re-declaration:
* Cannot be re-declared within the same scope.
#### Re-assignment:
* Cannot be reassigned. The value is constant after declaration.
* **Note:** For objects and arrays, the reference is constant, but the contents can still be modified.
```javascript
const z = 10;
if (true) {
    const z = 20;  // Different variable (block-scoped)
    console.log(z);  // 20
}
console.log(z);  // 10

const obj = {a: 1};
obj.a = 2;  // Allowed (mutating object property)
console.log(obj.a);  // 2

obj = {b: 2};  // Error! Cannot reassign the object reference.
```
*****

### 4. Summary Table

Feature |	`var` |	`let` |	`const`
--- | --- | --- | ---
**Scope** |	Function-scoped |	Block-scoped |	Block-scoped
**Hoisting** |	Yes (initialized as undefined) |	Yes (not initialized) |	Yes (not initialized)
**Re-declaration** |	Yes |	No |	No
**Re-assignment** |	Yes |	Yes |	No
