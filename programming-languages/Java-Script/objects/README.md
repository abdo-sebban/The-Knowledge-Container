# Objects in JavaScript

## Overview

In JavaScript, an **object** is used to store related data and functionality together.

An object contains **properties**, where each property has a **key** and a **value**.

For example:

```javascript

const user =
{
    name: "Abdo",
    age: 22,
    role: "Student"
};

```

You can think of it like this:

```text

user
│
├── name → "Abdo"
├── age  → 22
└── role → "Student"

```

Here:

* `name`, `age`, and `role` are **keys**.
* `"Abdo"`, `22`, and `"Student"` are **values**.

---

# Creating an Object

An object can be created using curly braces `{}`.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

```

The general structure is:

```javascript

const objectName =
{
    key: value,
    key: value
};

```

For example:

```javascript

const car =
{
    brand: "BMW",
    model: "M3",
    year: 2024
};

```

---

# Accessing Object Properties

There are two common ways to access a property.

## Dot Notation

```javascript

console.log(user.name);
console.log(user.age);

```

Output:

```text

Abdo
22

```

The syntax is:

```javascript

object.property

```

---

## Bracket Notation

You can also use square brackets:

```javascript

console.log(user["name"]);
console.log(user["age"]);

```

The result is the same.

The syntax is:

```javascript

object["property"]

```

---

# Dot Notation vs Bracket Notation

Both can access object properties:

```javascript

const user =
{
    name: "Abdo"
};

console.log(user.name);
console.log(user["name"]);

```

However, bracket notation is useful when the property name is stored inside a variable.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

const property = "name";

console.log(user[property]);

```

Output:

```text

Abdo

```

Here:

```javascript

user[property]

```

means:

```javascript

user["name"]

```

If you use dot notation:

```javascript

user.property

```

JavaScript looks for a property literally called `property`.

---

# Adding Properties

You can add a new property after creating an object.

```javascript

const user =
{
    name: "Abdo"
};

user.age = 22;

console.log(user);

```

The object now becomes:

```javascript

{
    name: "Abdo",
    age: 22
}

```

You can also use bracket notation:

```javascript

user["role"] = "Student";

```

---

# Modifying Properties

You can change the value of an existing property.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

user.age = 23;

console.log(user.age);

```

Output:

```text

23

```

---

# Deleting Properties

The `delete` operator removes a property from an object.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

delete user.age;

console.log(user);

```

The result is:

```javascript

{
    name: "Abdo"
}

```

---

# Object Methods

An object can also store functions.

When a function belongs to an object, it is called a **method**.

```javascript

const user =
{
    name: "Abdo",

    greet: function()
    {
        return "Hello!";
    }
};

console.log(user.greet());

```

Output:

```text

Hello!

```

Here:

```javascript

greet

```

is a method of the `user` object.

---

# The `this` Keyword

Inside an object method, `this` can refer to the object that is calling the method.

```javascript

const user =
{
    name: "Abdo",

    greet: function()
    {
        return "Hello, " + this.name;
    }
};

console.log(user.greet());

```

Output:

```text

Hello, Abdo

```

In this example:

```javascript

this.name

```

refers to:

```javascript

user.name

```

---

# Nested Objects

An object can contain another object.

```javascript

const user =
{
    name: "Abderrahmane",

    address:
    {
        city: "El Jadida",
        country: "Morocco"
    }
};

```

The structure looks like:

```text

user
│
├── name → "Abdo"
│
└── address
    │
    ├── city → "El Jadida"
    └── country → "Morocco"

```

You can access nested properties using:

```javascript

console.log(user.address.city);

```

Output:

```text

El Jadida

```

---

# Looping Through an Object

You can use a `for...in` loop to iterate through an object's properties.

```javascript

const user =
{
    name: "Abdo",
    age: 22,
    role: "Student"
};

for (let key in user)
{
    console.log(key);
}

```

Output:

```text

name
age
role

```

To access the values:

```javascript

for (let key in user)
{
    console.log(user[key]);
}

```

You can also access both:

```javascript

for (let key in user)
{
    console.log(key + ": " + user[key]);
}

```

Output:

```text

name: Abdo
age: 22
role: Student

```

---

# `Object.keys()`

`Object.keys()` returns an array containing all the keys of an object.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

console.log(Object.keys(user));

```

Output:

```text

["name", "age"]

```

---

# `Object.values()`

`Object.values()` returns an array containing all the values of an object.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

console.log(Object.values(user));

```

Output:

```text

["Abdo", 22]

```

---

# `Object.entries()`

`Object.entries()` returns an array containing both keys and values.

```javascript

const user =
{
    name: "Abdo",
    age: 22
};

console.log(Object.entries(user));

```

Output:

```text

[
    ["name", "Abdo"],
    ["age", 22]
]

```

---

# Important Concepts

An object is made of **key-value pairs**:

```javascript

const user =
{
    name: "Abdo"
};

```

```text

name  → key
"Abdo" → value

```

You can:

```text

Create   → {}
Access   → object.property
Add      → object.property = value
Modify   → object.property = newValue
Delete   → delete object.property

```

Objects can also contain:

* Strings
* Numbers
* Booleans
* Arrays
* Functions
* Other objects

For example:

```javascript

const user =
{
    name: "Abdo",
    age: 22,
    active: true,
    skills: ["C", "JavaScript", "Python"],

    address:
    {
        country: "Morocco"
    },

    greet: function()
    {
        return "Hello!";
    }
};

```

---

# Key Takeaways

* Objects store related data using key-value pairs.
* Properties can be accessed using dot notation or bracket notation.
* Properties can be added, modified, and deleted.
* Objects can contain functions called methods.
* `this` can be used inside methods to access properties of the calling object.
* Objects can contain other objects and arrays.
* `for...in` can be used to iterate through object properties.
* `Object.keys()`, `Object.values()`, and `Object.entries()` provide useful ways to work with objects.

---

## Simple Definition

> **An object is a collection of related data stored as key-value pairs.**
