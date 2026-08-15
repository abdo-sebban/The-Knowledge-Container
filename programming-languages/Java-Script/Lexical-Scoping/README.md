# Lexical Scoping in JavaScript

## Overview

**Lexical scoping** is the rule that determines which variables a function can access based on **where the function is written in the source code**.

In simple words:

> A function can access variables from its own scope and from the scopes surrounding it.

The word **lexical** refers to the position of the code. JavaScript determines the scope of variables based on where functions and variables are declared, not where a function is called.

---

## Global Scope

A variable declared outside of any function or block belongs to the **global scope**.

```javascript

let name = "John";

function    sayHello()
{
    console.log("Hello " + name);
}

sayHello();

```

Output:

```text
Hello John
```

The function `sayHello()` can access `name` because `name` exists in the outer, global scope.

```text

Global Scope
│
├── name = "John"
│
└── sayHello()
        │
        └── Can access name

```

---

## Local Scope

A variable declared inside a function belongs to that function's **local scope**.

```javascript

function sayHello()
{
    let name = "John";

    console.log("Hello " + name);
}

sayHello();

```

The variable `name` only exists inside `sayHello()`.

This will cause an error:

```javascript

console.log(name);

```

Because `name` is not accessible outside the function.

```text

sayHello()
│
└── name = "John"

```

The variable exists only inside this scope.

---

## Nested Scope

An inner function can access variables from its outer function.

```javascript

function outer()
{
    let name = "John";

    function inner()
    {
        console.log("Hello " + name);
    }

    inner();
}

outer();

```

The `inner()` function can access `name` because it was defined inside `outer()`.

```text

outer()
│
├── name = "John"
│
└── inner()
        │
        └── Can access name

```

However, the outer function cannot access variables declared only inside the inner function.

```javascript

function outer()
{
    function inner()
    {
        let message = "Hello";
    }

    console.log(message); // Error
}

```

Scope works from **inside to outside**, not from outside to inside.

---

## Block Scope

Variables declared with `let` and `const` can also be limited to a block.

A block is usually defined using curly braces:

```javascript

{
    // Block
}

```

For example:

```javascript

if (true)
{
    let message = "Hello";

    console.log(message);
}

console.log(message); // Error

```

The variable `message` only exists inside the `if` block.

```text

if block
│
└── message = "Hello"

```

Once outside the block, `message` is no longer accessible.

---

## How JavaScript Looks for Variables

When JavaScript needs a variable, it looks for it starting from the current scope.

For example:

```javascript

let x = 10;

function    outer()
{
    let y;
    
    y = 20;

    function inner()
    {
        let z;
        
        z = 30;

        console.log(x);
        console.log(y);
        console.log(z);
    }

    inner();
}

outer();

```

The `inner()` function can access:

```text

z → Its own scope
y → Outer function scope
x → Global scope

```

You can visualize it like this:

```text

Global Scope
│
├── x = 10
│
└── outer()
    │
    ├── y = 20
    │
    └── inner()
        │
        └── z = 30

```

`inner()` can look outward through the scope chain.

---

## Important Rule

The scope of a function depends on **where the function is defined**, not where it is called.

This is the main idea behind lexical scoping.

```javascript

function outer()
{
    let message;

    message = "Hello"

    function inner()
    {
        console.log(message);
    }

    return (inner);
}

const myFunction = outer();

myFunction();

```

Even though `myFunction()` is called outside `outer()`, the function was originally defined inside `outer()`. Therefore, it can access `message`.

This behavior is also closely related to **closures**.

---

## Lexical Scope and Closures

Lexical scoping allows an inner function to access variables from its outer scope.

A **closure** happens when a function keeps access to those outer variables even after the outer function has finished executing.

Example:

```javascript

function createCounter(n)
{
    return function()
    {
        return (n++);
    };
}

const counter = createCounter(10);

console.log(counter()); // 10
console.log(counter()); // 11
console.log(counter()); // 12

```

The returned function can still access `n` because of lexical scoping, and it keeps access to that variable through a closure.

```text
Lexical Scoping
        ↓
Inner function can access outer variables
        ↓
Closure
        ↓
The function keeps access to those variables
```

---

## Key Takeaways

* Lexical scope determines variable accessibility based on where code is written.
* A function can access variables from its own scope.
* An inner function can access variables from its outer scope.
* Outer scopes cannot directly access variables declared only inside inner scopes.
* Global variables can generally be accessed from nested scopes.
* `let` and `const` create block-scoped variables.
* Lexical scoping is an important concept for understanding closures.

---

## Simple Definition

> **Lexical scoping means that a function can access variables based on where the function was defined in the code.**

---

## References

* [Lexical Scope in JavaScript — GeeksforGeeks](https://www.geeksforgeeks.org/javascript/lexical-scope-in-javascript/)
