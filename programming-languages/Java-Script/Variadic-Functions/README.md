# Variadic Functions in JavaScript

## Overview

A **variadic function** is a function that can accept a variable number of arguments. Instead of defining a fixed number of parameters, the function can work with however many arguments are provided when it is called.

For example:

```javascript
sum(1, 2);
sum(1, 2, 3);
sum(1, 2, 3, 4, 5);
```

All of these calls can be handled by the same variadic function.

---

## Using the `arguments` Object

In regular JavaScript functions, the `arguments` object provides access to all arguments passed to the function.

```javascript

function sum()
{
    let Result;
    
    Result = 0;

    for (let i = 0; i < arguments.length; i++)
    {
        Result += arguments[i];
    }

    return (Result);
}

console.log(sum(1, 2, 3));       // Result = 1 + 2 + 3 = 6
console.log(sum(1, 2, 3, 4));    // Result = 1 + 2 + 3 + 4 = 10

```

The `arguments` object is a local variable available within all non-arrow functions.
You can refer to a function's arguments inside that function by using its arguments object.
It has entries for each argument the function was called with, with the first entry's index at 0.

---

## Using Rest Parameters

The modern and generally cleaner approach is to use **rest parameters**.

```javascript

function sum(...numbers)
{
    let Result = 0;

    for (const number of numbers)
    {
        Result += number;
    }

    return (Result);
}

console.log(sum(1, 2, 3));       // Result = 1 + 2 + 3 = 6
console.log(sum(1, 2, 3, 4));    // Result = 1 + 2 + 3 + 4 = 10

```

The `...numbers` syntax collects all remaining arguments into an actual array.

This allows us to use array methods such as:

```javascript

function sum(...numbers)
{
    return (numbers.reduce((Result, number) => Result + number, 0));
}

```

---

## `arguments` vs Rest Parameters

| `arguments`                             | Rest Parameters                 |
| --------------------------------------- | ------------------------------- |
| Available inside regular functions      | Explicitly declared using `...` |
| Array-like object                       | Real array                      |
| Older approach                          | Modern approach                 |
| Does not provide array methods directly | Supports array methods          |
| Not available in arrow functions        | Works with arrow functions      |

### Example with an Arrow Function

```javascript

const sum = (...numbers) => { return numbers.reduce((total, number) => total + number, 0); };


console.log(sum(10, 20, 30)); // 10 + 20 + 30 => 60

```

---

## Key Takeaways

* Variadic functions can accept a variable number of arguments.
* The modern approach is to use **rest parameters**.
* Rest parameters collect arguments into a real array.
* Rest parameters are generally easier to read and work with.

---

## References

* [Variadic Functions in JavaScript - GeeksforGeeks](https://www.geeksforgeeks.org/javascript/variadic-functions-in-javascript/)
