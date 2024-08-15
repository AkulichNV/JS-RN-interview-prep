## 1. Global Context

* In the Global Scope (`this` refers to the global object):
```javascript
console.log(this); // Window object in browsers
```

## 2. Function Context
* In a Regular Function (`this` refers to the global object in non-strict mode, or `undefined` in strict mode):
```javascript
function showThis() {
  console.log(this);
}
showThis(); // Window (or global object) in non-strict mode, undefined in strict mode
```

* Strict Mode Example:
```javascript
'use strict';
function showThis() {
  console.log(this);
}
showThis(); // undefined
```

## 3. Object Method Context
* In a Method of an Object (`this` refers to the object that owns the method):
```javascript
const obj = {
  name: 'Alice',
  greet() {
    console.log(this.name);
  }
};
obj.greet(); // 'Alice'
```

## 4. Constructor Function Context
* In a Constructor Function (`this` refers to the newly created instance):
```javascript
function Person(name) {
  this.name = name;
}

const person1 = new Person('Bob');
console.log(person1.name); // 'Bob'
```

## 5. Class Context
* In a Class Method (`this` refers to the instance of the class):
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(this.name);
  }
}

const person1 = new Person('Charlie');
person1.greet(); // 'Charlie'
```

## 6. Arrow Function Context
* In Arrow Functions (`this` is lexically inherited from the surrounding scope):
```javascript
const obj = {
  name: 'Dave',
  greet: function() {
    const innerFunc = () => {
      console.log(this.name);
    };
    innerFunc();
  }
};
obj.greet(); // 'Dave'
```

## 7. Event Handlers in DOM
* In Event Handlers (`this` refers to the element that received the event):
```javascript
const button = document.querySelector('button');
button.addEventListener('click', function() {
  console.log(this); // The button element
});
```
* Arrow Functions in Event Handlers (Inherits `this` from the lexical scope, usually the window or enclosing object):
```javascript
button.addEventListener('click', () => {
  console.log(this); // Usually refers to the window or enclosing object
});
```

## 8. Explicit Binding (Using `call`, `apply`, and `bind`)
* Using `call` and `apply` (Manually sets `this`):
```javascript
function greet() {
  console.log(this.name);
}

const person = { name: 'Eve' };

greet.call(person); // 'Eve'
greet.apply(person); // 'Eve'
```
* Using `bind` (Returns a new function with `this` bound):
```javascript
const greetBound = greet.bind(person);
greetBound(); // 'Eve'
```

## 9. Default Binding
* Function Invocation without any object (`this` refers to the global object in non-strict mode or `undefined` in strict mode):
```javascript
function showThis() {
  console.log(this);
}

showThis(); // Window (or global object), or undefined in strict mode
```

## 10. Implicit Binding
* When a function is called as a method of an object (`this` refers to the object):
```javascript
const user = {
  name: 'Frank',
  getName() {
    console.log(this.name);
  }
};

user.getName(); // 'Frank'
```

## 11. `this` in Prototypes
* In a method added to a prototype (`this` refers to the instance):
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(this.name);
};

const person1 = new Person('George');
person1.greet(); // 'George'
```

## 12. `this` in SetTimeout
* In a `setTimeout` function (non-arrow function, `this` defaults to the global object or `undefined` in strict mode):
```javascript
const obj = {
  name: 'Helen',
  greet() {
    setTimeout(function() {
      console.log(this.name);
    }, 1000);
  }
};
obj.greet(); // undefined (or error in strict mode)
```

* Arrow Function in `setTimeout` (Inherits `this` from the surrounding scope):
```javascript
const obj = {
  name: 'Ian',
  greet() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};
obj.greet(); // 'Ian'
```

## 13. `this` in Closures
* In a Closure (using `self` or `that` to retain `this`):
```javascript
const obj = {
  name: 'Jack',
  greet() {
    const self = this;
    function innerFunc() {
      console.log(self.name);
    }
    innerFunc();
  }
};
obj.greet(); // 'Jack'
```

## 14. `this` in Object Assignments
* Method assigned to a variable loses its original `this`:
```javascript
const obj = {
  name: 'Karen',
  greet() {
    console.log(this.name);
  }
};

const greetFunction = obj.greet;
greetFunction(); // undefined or throws error in strict mode
```
* To retain `this`, use `bind`:
```javascript
const greetFunctionBound = obj.greet.bind(obj);
greetFunctionBound(); // 'Karen'
```

## 15. `this` in Callbacks
* `this` in callbacks depends on how they are invoked:
```javascript
const obj = {
  name: 'Laura',
  greet(callback) {
    callback();
  }
};

const person = {
  name: 'Matt',
  sayName() {
    console.log(this.name);
  }
};

obj.greet(person.sayName); // undefined (or throws error in strict mode)
```

* Using `bind` to ensure correct `this`:
```javascript
obj.greet(person.sayName.bind(person)); // 'Matt'
```

## Conclusion
* **Lexical Scoping vs. Dynamic Scoping:** Arrow functions use lexical scoping, whereas regular functions use dynamic scoping.
* **Context Switching:** Always pay attention to how and where a function is invoked, as it significantly affects the value of this.
