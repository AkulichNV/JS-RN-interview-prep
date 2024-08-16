## 1. Overview
* **JavaScript is single-threaded:** It can only execute one task at a time.
* **Event Loop:** Manages the execution of multiple chunks of code (callbacks) over time, handling asynchronous operations.

## 2. Call Stack
* **Call Stack:** A data structure that tracks function calls in the order they need to be executed.
* When a function is called, it is pushed onto the stack.
* When the function finishes execution, it is popped off the stack.

## 3. Web APIs
* **Web APIs:** Browser-provided features like `setTimeout`, `DOM events`, `fetch`, etc., are not part of the JavaScript language but can be used in JavaScript code.

## 4. Task Queue (Callback Queue)
* **Task Queue:** Holds messages (callbacks) from asynchronous operations (e.g., `setTimeout`, `event handlers`) that are ready to be executed.
* **Microtask Queue:** A special task queue for microtasks like `Promises` and `MutationObserver`.

## 5. Event Loop Execution
* **Execute Stack:** The event loop starts by executing all code on the call stack.
* **Process Task Queue:** Once the call stack is empty, the event loop checks the task queue.
* **Process Microtask Queue:** The microtask queue has higher priority than the task queue. The event loop checks and processes all microtasks before moving to the next task in the task queue.
* **Repeat:** The event loop continues this cycle until there are no tasks remaining.

## 6. Example: Event Loop in Action
```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout Callback');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise Callback');
});

console.log('End');
```
* **Output Order:**

* `Start`
* `End`
* `Promise Callback`
* `Timeout Callback`

## 7. Key Concepts
* Call Stack runs first.
* **Microtasks** (Promises) have priority over macrotasks (setTimeout).
* **Macrotasks** include tasks from `setTimeout`, `setInterval`, `I/O`(Handles callbacks from I/O operations like reading files, network requests, etc.), etc.
* **Microtasks** include `Promise callbacks`(`.then()`, `.catch()`, and `.finally()`), `MutationObserver`.
  
## 8. Important Points
* **Blocking the Call Stack:** Long-running tasks block the event loop, making the UI unresponsive.
* **Task Prioritization:** Understanding task and microtask queues helps avoid race conditions and manage async operations efficiently.
* **Execution Order:** Microtasks always run before the next macrotask.
