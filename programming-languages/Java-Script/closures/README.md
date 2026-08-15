# Closures in JavaScript

## Overview

A **closure** is created when a function keeps access to variables from its outer scope, even after the outer function has finished executing.

In simple words:

> A closure allows a function to remember and access variables from the scope where it was created.

Closures are possible because of **lexical scoping**.

---

## A Simple Example

Consider the following code:

```javascript

function outer()
{
    let message = "Hello";

    function inner()
    {
        console.log(message);
    }

    inner();
}

outer();

```

The `inner()` function can access the `message` variable because it was defined inside `outer()`.

This is an example of **lexical scoping**.

```text

outer()
│
├── message = "Hello"
│
└── inner()
        │
        └── Can access message

```

---

## Creating a Closure

Now let's return the inner function:

```javascript
function outer()
{
    let message = "Hello";

    return function()
    {
        return message;
    };
}

const inner = outer();

console.log(inner());

```

Output:

```text

Hello

```

Even though `outer()` has already finished executing, the returned function can still access `message`.

This behavior is called a **closure**.

```text

outer()
│
├── message = "Hello"
│
└── returns inner function
        │
        └── keeps access to message

```

---

## Step by Step

When this code runs:

```javascript

const inner = outer();

```

JavaScript does the following:

```text

1. Call outer()

2. Create: message = "Hello"

3. Create the inner function

4. Return the inner function

5. Store it in: inner

```

Then:

```javascript

console.log(inner());

```

The function can still access:

```javascript

message

```

Even though `outer()` has finished.

```text

outer() finished
        ↓
The returned function still exists
        ↓
It keeps access to message
        ↓
This is a closure

```

---

# A Practical Example: Counter

Closures are useful when a function needs to remember a value between multiple calls.

```javascript

function createCounter(n)
{
    return function()
    {
        return (n++);
    };
}

const counter = createCounter(10);

console.log(counter());
console.log(counter());
console.log(counter());

```

Output:

```text

10
11
12

```

### What happens?

When we call:

```javascript

const counter = createCounter(10);

```

The value of `n` is:

```text

n = 10

```

The returned function keeps access to `n`.

Each time we call:

```javascript

counter();

```

The same variable is used.

```text

First call:

n = 10
return 10
n becomes 11

```

```text

Second call:

n = 11
return 11
n becomes 12

```

```text

Third call:

n = 12
return 12
n becomes 13

```

The function remembers the value of `n` between calls.

This is a closure.

---

## Multiple Closures

Each call to the outer function creates its own separate closure.

```javascript

function createCounter(n)
{
    return function()
    {
        return (n++);
    };
}

const counter1 = createCounter(0);
const counter2 = createCounter(10);

console.log(counter1()); // 0
console.log(counter1()); // 1

console.log(counter2()); // 10
console.log(counter2()); // 11

```

`counter1` and `counter2` do not share the same `n`.

You can think of them like this:

```text

counter1
│
└── remembers n = 0


counter2
│
└── remembers n = 10

```

Each closure has access to its own variables.

---

# Closures and Lexical Scoping

Closures and lexical scoping are closely related, but they are not exactly the same thing.

## Lexical Scoping

Lexical scoping determines which variables a function can access based on **where the function is defined**.

```javascript

function outer()
{
    let x = 10;

    function inner()
    {
        return (x);
    }
}

```

`inner()` can access `x` because it was defined inside `outer()`.

## Closure

A closure allows the function to keep access to that variable after the outer function has finished.

```javascript

function outer()
{
    let x = 10;

    return function()
    {
        return (x);
    };
}

const inner = outer();

console.log(inner()); // 10

```

The difference can be summarized as:

```text

Lexical Scoping
        ↓
Determines what variables a function can access
        ↓
Closure
        ↓
The function keeps access to those variables

```

---

# Why Are Closures Useful?

Closures are commonly used to:

* Preserve state between function calls.
* Create private variables.
* Create function factories.
* Build counters.
* Manage callbacks and event handlers.

---

## Example: Private Variable

A variable inside a function cannot be accessed directly from outside.

```javascript

function createCounter()
{
    let count = 0;

    return function()
    {
        count++;

        return (count);
    };
}

const counter = createCounter();

console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

The variable `count` cannot be accessed directly:

```javascript

console.log(count); // Error

```

Only the returned function can access and modify it.

---

# Key Takeaways

* A closure is created when a function keeps access to variables from its outer scope.
* The function can access those variables even after the outer function has finished.
* Closures are based on lexical scoping.
* Closures can be used to preserve state between function calls.
* Each closure can maintain its own independent state.
* Closures are commonly used for counters, private variables, callbacks, and function factories.

---

## Simple Definition

> **A closure is a function that remembers and can access variables from its outer scope, even after the outer function has finished executing.**
