## 1. Global Scope vs. Functional Scope

### Global Scope:
* Variables declared outside of any function have global scope.
* These variables are accessible from anywhere in the code.
* They persist for the duration of the program.
```javascript
var globalVar = "I am global";

function test() {
    console.log(globalVar); // Accessible here
}

test();
console.log(globalVar); // Accessible here too
```

### Functional Scope:
* Variables declared inside a function are scoped to that function.
* They are only accessible within that function and its nested scopes.
* Variables declared with `var` have functional scope.
```javascript
function myFunction() {
    var localVar = "I am local";
    console.log(localVar); // Accessible here
}

myFunction();
console.log(localVar); // Error: localVar is not defined
```

## 2. Variable Visibility Areas

### Global Variables:
* Visible throughout the entire program, unless shadowed by a local variable of the same name.
### Local Variables:
* Visible only within the function where they are declared.
* If a local variable has the same name as a global variable, it "shadows" the global variable within its scope.
```javascript
var myVar = "Global";

function test() {
    var myVar = "Local";
    console.log(myVar); // "Local" - shadows the global variable
}

test();
console.log(myVar); // "Global"
```

## 3. Working with Nested Scopes

### Nested Scopes:
* Functions can be nested, creating multiple levels of scope.
* Inner functions have access to variables of their outer functions.
```javascript
function outerFunction() {
    var outerVar = "I am outer";
    
    function innerFunction() {
        var innerVar = "I am inner";
        console.log(outerVar); // "I am outer" - can access outerVar
        console.log(innerVar); // "I am inner" - can access innerVar
    }

    innerFunction();
    console.log(innerVar); // Error: innerVar is not defined
}

outerFunction();
```
### Closure:
* A closure is a function that remembers the scope in which it was created, even after that scope has finished executing.
```javascript
function outerFunction() {
    var outerVar = "I am outer";

    return function innerFunction() {
        console.log(outerVar); // "I am outer" - closure retains access to outerVar
    };
}

var myClosure = outerFunction();
myClosure(); // "I am outer"
```

## 4. Important Points to Remember

### Function Declarations and Hoisting:
* Function declarations are hoisted to the top of their scope.
* This means they can be called before their actual definition in the code.
```javascript
hoistedFunction(); // Works even though defined below

function hoistedFunction() {
    console.log("This is hoisted!");
}
```

### `var` vs. `let`/`const` (Block Scope):
* `var` has function scope, while `let` and `const` have block scope.
* Block scope means variables are confined to the block `{}` where they are declared.
```javascript
function testVar() {
    if (true) {
        var x = 10;
    }
    console.log(x); // 10 - `var` is function-scoped
}

function testLet() {
    if (true) {
        let y = 10;
    }
    console.log(y); // Error: y is not defined - `let` is block-scoped
}

testVar();
testLet();
```
