Give 50 killer MCQs (exam-level)

🧪 Do trick code prediction questions

🎯 Focus only on sir’s favorite traps


### Q1. What is JavaScript?

**A:** A single-threaded, interpreted, event-driven language used for web development.

---

### Q2. Is JavaScript synchronous or asynchronous?

**A:** Synchronous by default, but can handle async operations using callbacks, promises, and async/await.

---

### Q3. What does “single-threaded” mean?

**A:** JavaScript can execute **one task at a time** on the main thread.

---

### Q4. What is hoisting?

**A:** Variable and function declarations are moved to the top of their scope during compilation.

---

### Q5. Difference between `var`, `let`, and `const`?

**A:**

* `var` → function scoped
* `let` → block scoped
* `const` → block scoped, cannot be reassigned

---

### Q6. What is a closure?

**A:** A function that remembers variables from its outer scope even after execution.

---

### Q7. What is a callback?

**A:** A function passed as an argument to be executed later.

---

### Q8. What is callback hell?

**A:** Nested callbacks that make code unreadable and hard to maintain.

---

### Q9. What is a Promise?

**A:** An object representing the eventual completion or failure of an async operation.

---

### Q10. Promise states?

**A:**

* Pending
* Fulfilled
* Rejected

---

### Q11. What is `async/await`?

**A:** Syntax sugar over promises that makes async code look synchronous.

---

### Q12. What is the event loop?

**A:** Mechanism that handles async operations by managing the call stack and task queues.

---

### Q13. Difference between `==` and `===`?

**A:**

* `==` → loose comparison
* `===` → strict comparison

---

### Q14. What is `this`?

**A:** Refers to the object that is executing the current function.

---

### Q15. What is DOM?

**A:** Document Object Model — a tree representation of HTML.

---

### Q16. What is AJAX?

**A:** Asynchronous JavaScript and XML — updating parts of a page without reload.

---

### Q17. What is CORS?

**A:** Browser security rule that controls cross-origin requests.

---

### Q18. What is debouncing?

**A:** Delays execution until the event stops firing.

---

### Q19. What is throttling?

**A:** Limits execution to once per time interval.

---

### Q20. Difference between `map`, `filter`, `reduce`?

**A:**

* `map` → transform
* `filter` → select
* `reduce` → accumulate

---

# 2️⃣ Async JavaScript & Event Loop (DEEP BUT SIMPLE)

## 2.1 Why async JS is needed

JavaScript runs on **one thread**.

Blocking code like this is bad:

```js
while(true) {}
```

Async lets JS:

* Request data
* Wait without blocking
* Continue executing other code

---

## 2.2 Core components of async JS

### 1️⃣ Call Stack

* Where functions are executed
* LIFO (Last In, First Out)

```js
function a() {
  b();
}
function b() {
  console.log("Hi");
}
a();
```

Stack:

```
a()
b()
console.log()
```

---

### 2️⃣ Web APIs (Browser)

* `setTimeout`
* `fetch`
* `XMLHttpRequest`
* DOM events

They run **outside** the call stack.

---

### 3️⃣ Callback / Task Queue

* Holds completed async callbacks
* Example: `setTimeout`

---

### 4️⃣ Microtask Queue (VERY IMPORTANT)

* Holds:

  * Promise `.then()`
  * `async/await`

⚠️ Microtasks have **higher priority** than tasks.

---

### 5️⃣ Event Loop

* Constantly checks:

  * Is call stack empty?
  * Then moves microtasks
  * Then moves tasks

---

## 2.3 Event Loop Diagram (Mental Model)

```
        ┌────────────┐
        │ Call Stack │
        └─────┬──────┘
              │
     ┌────────▼─────────┐
     │   Event Loop     │
     └────────┬─────────┘
              │
   ┌──────────▼───────────┐
   │   Microtask Queue    │ (Promises)
   └──────────┬───────────┘
              │
   ┌──────────▼───────────┐
   │    Task Queue        │ (setTimeout)
   └──────────────────────┘
```

---

## 2.4 Code example (INTERVIEW FAVORITE 🔥)

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```

### Execution order:

```
A
D
C
B
```

### Why?

1. Sync code → `A`, `D`
2. Microtasks → `C`
3. Tasks → `B`

---

## 2.5 `async/await` under the hood

```js
async function test() {
  console.log("1");
  await Promise.resolve();
  console.log("2");
}

test();
console.log("3");
```

### Output:

```
1
3
2
```

👉 `await` pauses function execution and pushes the rest into microtask queue.

---

## 2.6 Interview one-liners (MEMORIZE)

* JS is **single-threaded but non-blocking**
* Promises go to **microtask queue**
* `setTimeout` goes to **task queue**
* Microtasks run **before** tasks
* Event loop moves tasks only when stack is empty

---

## 3️⃣ Final confidence checklist ✅

If you can explain:
✔ Call stack
✔ Web APIs
✔ Event loop
✔ Microtask vs Task queue
✔ Output-based questions

