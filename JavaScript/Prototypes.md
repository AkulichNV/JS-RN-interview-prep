## 1. What are Prototypes?

* Prototypes are the mechanism by which JavaScript objects inherit properties and methods from one another.
* Every JavaScript object has a prototype property, which is a reference to another object.

## 2. Prototype Chain

* When you try to access a property of an object, JavaScript will look for it in the object itself. If it doesn’t find it, it will look for it in the object’s prototype, and so on, until it reaches `Object.prototype`, which is the top of the prototype chain.
```javascript
const obj = {};
console.log(obj.__proto__ === Object.prototype); // true
```

## 3. Creating Objects with Prototypes

#### Using Object Literals
```javascript
const person = {
  name: 'John',
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
};
```

#### Using Constructor Functions
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const john = new Person('John');
john.greet(); // Hello, my name is John
```

#### Using `Object.create()`
```javascript
const personProto = {
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

const john = Object.create(personProto);
john.name = 'John';
john.greet(); // Hello, my name is John
```

## 4. Prototype Property

* The `prototype` property is used primarily for functions that are intended to be used as constructors.
```javascript
function Dog(name) {
  this.name = name;
}

Dog.prototype.bark = function() {
  console.log(`${this.name} says woof!`);
};

const rex = new Dog('Rex');
rex.bark(); // Rex says woof!
```

## 5. `__proto__` vs `prototype`

* **`__proto__`:** The actual object that is used in the lookup chain to resolve methods, etc. It is an internal property of the object (non-standard in older implementations).
* **`prototype`:** A property of functions that is used when you create a new object with new. It defines the prototype of instances created by that constructor function.
```javascript
console.log(rex.__proto__ === Dog.prototype); // true
```

## 6. Prototype Inheritance

* You can create an inheritance chain by setting the prototype of one object to be an instance of another.
```javascript
function Animal() {}

Animal.prototype.eat = function() {
  console.log('Eating...');
};

function Cat(name) {
  this.name = name;
}

Cat.prototype = Object.create(Animal.prototype);
Cat.prototype.constructor = Cat;

Cat.prototype.meow = function() {
  console.log(`${this.name} says meow!`);
};

const kitty = new Cat('Kitty');
kitty.eat();  // Eating...
kitty.meow(); // Kitty says meow!
```

## 7. Checking Prototype Chain

* **`instanceof`:** Checks if an object is an instance of a constructor.
* **`isPrototypeOf`:** Checks if an object exists within another object's prototype chain.
```javascript
console.log(kitty instanceof Cat);    // true
console.log(Animal.prototype.isPrototypeOf(kitty)); // true
```

## 8. Extending Built-in Prototypes (Not Recommended)

* You can extend built-in objects like `Array`, `String`, etc., but it's usually not recommended as it can cause issues in your code or with other libraries.
```javascript
Array.prototype.sum = function() {
  return this.reduce((acc, num) => acc + num, 0);
};

const numbers = [1, 2, 3, 4];
console.log(numbers.sum()); // 10
```
