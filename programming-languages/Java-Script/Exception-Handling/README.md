# Exception Handling in JavaScript

## Overview

While a JavaScript program is running, unexpected problems can occur.

For example:

* A variable does not exist.
* A function receives invalid input.
* A number is outside an expected range.
* Invalid JSON data is provided.

JavaScript uses **exceptions** to represent these errors.

Exception handling allows us to detect and handle errors instead of letting the program stop unexpectedly.

The main keywords used for exception handling are:

```text

try
catch
finally
throw

```

---

# What Is an Exception?

An **exception** is a problem that occurs while the program is running.

For example:

```javascript

console.log(user);

```

If `user` does not exist, JavaScript throws an error.

Conceptually:

```text

Program is running
        ↓
Something goes wrong
        ↓
An exception is thrown
        ↓
The program stops unless the error is handled

```

---

# `try` and `catch`

The `try` block contains code that may cause an error.

The `catch` block handles the error if one occurs.

```javascript

try
{
    // Code that may cause an error
}
catch (error)
{
    // Handle the error
}

```

Example:

```javascript

try
{
    console.log(user);
}
catch (error)
{
    console.log("An error occurred");
}

```

Instead of stopping the program, JavaScript moves to the `catch` block.

---

## Accessing the Error

The `catch` block receives information about the error.

```javascript

try
{
    console.log(user);
}
catch (error)
{
    console.log(error);
}

```

You can also access the error message:

```javascript

try
{
    console.log(user);
}
catch (error)
{
    console.log(error.message);
}

```

Example output:

```text

user is not defined

```

---

# How `try...catch` Works

```javascript

try
{
    console.log("Start");

    console.log(user);

    console.log("End");
}
catch (error)
{
    console.log("Something went wrong");
}

```

The execution flow is:

```text
Start
  ↓
console.log(user)
  ↓
Error occurs
  ↓
Skip the rest of the try block
  ↓
Go to catch
  ↓
"Something went wrong"

```

The following line will not execute:

```javascript

console.log("End");

```

Because execution immediately moves to `catch` when the exception occurs.

---

# The `finally` Block

The `finally` block runs whether an error occurs or not.

```javascript

try
{
    console.log("Trying...");
}
catch (error)
{
    console.log("An error occurred");
}
finally
{
    console.log("This always runs");
}

```

Output:

```text

Trying...
This always runs

```

Now let's cause an error:

```javascript

try
{
    console.log(user);
}
catch (error)
{
    console.log("An error occurred");
}
finally
{
    console.log("This always runs");
}

```

Output:

```text

An error occurred
This always runs

```

You can think of it like this:

```text
           try
            │
     ┌──────┴──────┐
     │             │
 No Error        Error
     │             │
     │           catch
     │             │
     └──────┬──────┘
            │
         finally
            │
            ▼
          Continue

```

---

# The `throw` Keyword

JavaScript automatically throws some errors.

However, you can also create your own errors using `throw`.

```javascript

throw new Error("Something went wrong");

```

Example:

```javascript

function divide(a, b)
{
    if (b === 0)
    {
        throw new Error("Cannot divide by zero");
    }

    return a / b;
}

```

Now we can handle the error:

```javascript

try
{
    console.log(divide(10, 0));
}
catch (error)
{
    console.log(error.message);
}

```

Output:

```text

Cannot divide by zero

```

The execution flow is:

```text

    divide(10, 0)
        │
        ▼
    b === 0 ?
        │
       Yes
        │
        ▼
    throw Error
        │
        ▼
    catch(error)
        │
        ▼
Display error message

```

---

# `Error` Objects

JavaScript provides built-in error objects.

The most common ones include:

## `Error`

A general error.

```javascript

throw new Error("Something went wrong");

```

## `TypeError`

Occurs when a value has an unexpected type.

```javascript

let number = 10;

number.toUpperCase();

```

## `ReferenceError`

Occurs when trying to access a variable that does not exist.

```javascript

console.log(user);

```

## `SyntaxError`

Occurs when JavaScript code has invalid syntax.

```javascript

if (true)
{
    console.log("Hello");
}

```

## `RangeError`

Occurs when a value is outside an allowed range.

---

# Checking Error Types

You can check the type of an error using `instanceof`.

```javascript

try
{
    console.log(user);
}
catch (error)
{
    if (error instanceof ReferenceError)
    {
        console.log("The variable does not exist");
    }
    else
    {
        console.log("Another error occurred");
    }
}

```

---

# A Practical Example

Imagine a function that requires a valid age.

```javascript

function checkAge(age)
{
    if (typeof age !== "number")
    {
        throw new TypeError("Age must be a number");
    }

    if (age < 0)
    {
        throw new RangeError("Age cannot be negative");
    }

    return "Valid age";
}

```

We can handle different errors:

```javascript

try
{
    console.log(checkAge(-10));
}
catch (error)
{
    if (error instanceof TypeError)
    {
        console.log("Type Error: " + error.message);
    }
    else if (error instanceof RangeError)
    {
        console.log("Range Error: " + error.message);
    }
    else
    {
        console.log("Unknown Error");
    }
}

```

Output:

```text

Range Error: Age cannot be negative

```

---

# `throw` vs `return`

These two are different.

## `return`

`return` sends a normal value back from a function.

```javascript

function divide(a, b)
{
    if (b === 0)
    {
        return null;
    }

    return a / b;
}

```

## `throw`

`throw` stops the normal execution and creates an exception.

```javascript

function divide(a, b)
{
    if (b === 0)
    {
        throw new Error("Cannot divide by zero");
    }

    return a / b;
}

```

The difference:

```text

return
│
└── Normal result


throw
│
└── Something went wrong
    │
    └── Can be handled with catch

```

---

# Important Example

```javascript

function getUser(user)
{
    if (!user)
    {
        throw new Error("User is required");
    }

    return user;
}

try
{
    console.log(getUser(null));
}
catch (error)
{
    console.error(error.message);
}
finally
{
    console.log("Function execution finished");
}

```

The flow:

```text

getUser(null)
      │
      ▼
Is user valid?
      │
      ▼
     No
      │
      ▼
throw Error
      │
      ▼
    catch
      │
      ▼
Display error message
      │
      ▼
    finally
      │
      ▼
Execution finished

```

---

# Summary

JavaScript exception handling mainly uses four keywords:

| Keyword   | Purpose                               |
| --------- | ------------------------------------- |
| `try`     | Contains code that may throw an error |
| `catch`   | Handles the error                     |
| `throw`   | Creates an exception manually         |
| `finally` | Runs whether an error occurs or not   |

The general structure is:

```javascript

try
{
    // Code that may cause an error
}

catch (error)
{
    // Handle the error
}

finally
{
    // Code that always runs
}

```

---

# Key Takeaways

* An exception is an error that occurs while a program is running.
* Use `try` to wrap code that may throw an exception.
* Use `catch` to handle the exception.
* Use `throw` to create your own exceptions.
* Use `finally` for code that should run regardless of whether an error occurs.
* The `error` object can provide information such as `error.name` and `error.message`.
* JavaScript provides built-in error types such as `Error`, `TypeError`, `ReferenceError`, and `RangeError`.

---

## Simple Definition

> **Exception handling is a way to detect and handle errors so that a program can respond to problems in a controlled way.**

---

## References

* [MDN: try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
* [MDN: Control Flow and Error Handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
