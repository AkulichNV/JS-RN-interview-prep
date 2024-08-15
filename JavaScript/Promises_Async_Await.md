## Promises

* A `Promise` is an object representing the eventual completion (or failure) of an asynchronous operation.

#### Creating a Promise
```javascript
const myPromise = new Promise((resolve, reject) => {
    if (/* operation successful */) {
        resolve("Success!");
    } else {
        reject("Failure!");
    }
});
```

#### Using a Promise
```javascript
myPromise
    .then(value => {
        console.log(value); // Success!
    })
    .catch(error => {
        console.error(error); // Failure!
    })
    .finally(() => {
        console.log("Promise has been handled");
    });
```

#### Common Promise Methods

* **`then()`:** Attaches callbacks for the resolution and/or rejection of the Promise.
```javascript
myPromise.then(onFulfilled, onRejected);
```
* **`catch()`:** Attaches a callback for only the rejection of the Promise.
```javascript
myPromise.catch(onRejected);
```
* **`finally()`:** Attaches a callback that is executed regardless of the Promise's outcome.
```javascript
myPromise.finally(onFinally);
```
* **`Promise.all()`:** Waits for all promises to be fulfilled or any to be rejected.
```javascript
Promise.all([promise1, promise2])
    .then(results => {
        console.log(results); // Array of results from promises
    })
    .catch(error => {
        console.error(error);
    });
```
* **`Promise.race()`:** Resolves or rejects as soon as one of the promises resolves or rejects.
```javascript
Promise.race([promise1, promise2])
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.error(error);
    });
```
* **`Promise.allSettled()`:** Waits for all promises to either resolve or reject and returns an array of the results.
```javascript
Promise.allSettled([promise1, promise2])
    .then(results => {
        results.forEach(result => {
            if (result.status === "fulfilled") {
                console.log(result.value);
            } else {
                console.error(result.reason);
            }
        });
    });
```
* **`Promise.any()`:** Resolves as soon as any of the promises is fulfilled, or rejects if all of them are rejected.
```javascript
Promise.any([promise1, promise2])
    .then(result => {
        console.log(result); // First fulfilled promise
    })
    .catch(error => {
        console.error(error); // All promises were rejected
    });
```

## Async/Await

* async/await is syntactic sugar over promises that make asynchronous code look and behave more like synchronous code.

#### Basic Example

```javascript
async function fetchData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error fetching data:', error);
    } finally {
        console.log("Fetch attempt complete");
    }
}

fetchData();
```

#### Key Points

* **`async` keyword:** Declares an asynchronous function. This function returns a Promise.
```javascript
async function myAsyncFunction() {
    return "Hello, World!";
}

myAsyncFunction().then(value => console.log(value)); // "Hello, World!"
```
* **`await` keyword:** Pauses the execution of the async function until the promise is settled (fulfilled or rejected).
```javascript
async function myAsyncFunction() {
    const value = await somePromise();
    console.log(value);
}
```

#### Error Handling with Async/Await

```javascript
async function getData() {
    try {
        const data = await fetchData();
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
}

getData();
```

#### Using await with Promise.all()

```javascript
async function fetchMultipleData() {
    try {
        const [data1, data2] = await Promise.all([fetchData1(), fetchData2()]);
        console.log(data1, data2);
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}

fetchMultipleData();
```

## Common Patterns

### Sequential vs. Parallel Execution

#### Sequential Execution (Await in sequence):
```javascript
async function sequentialFetch() {
    const data1 = await fetchData1();
    const data2 = await fetchData2();
    console.log(data1, data2);
}
```

#### Parallel Execution (Awaiting multiple Promises):
```javascript
async function parallelFetch() {
    const [data1, data2] = await Promise.all([fetchData1(), fetchData2()]);
    console.log(data1, data2);
}
```
#### Looping with async/await
```javascript
async function processArray(array) {
    for (let item of array) {
        await processItem(item);
    }
}
```

#### Chaining Promises with Async/Await
```javascript
async function chainPromises() {
    const result1 = await firstAsyncFunction();
    const result2 = await secondAsyncFunction(result1);
    return result2;
}
```

#### Handling Timeouts
```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function timeoutExample() {
    await delay(3000); // Wait for 3 seconds
    console.log('3 seconds passed');
}
```

#### Error Handling in Loops
```javascript
async function processItems(items) {
    for (const item of items) {
        try {
            await processItem(item);
        } catch (error) {
            console.error(`Error processing ${item}:`, error);
        }
    }
}
```
