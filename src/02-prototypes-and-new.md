# Prototype & new

## Avoid Duplication with Prototype

What we really want to do is to store the `increment` function in just one object asnd have the interpreter, if it doesn't find the funciton on `user1`, look up to that object to check if it's there. How do we make this linK?

### Using the prototype chain

```js
const functionStore = {
    increment: function() { this.score++ },
    login: function() { console.log("You're logged in"); }
};

const user1 =  {
    name: "Phil",
    score: 4
}

user1.name // name is a property of user1 object
user1.increment // Error! increment is not!
```

We need to link `user1` and `functionStore` so that the interpreter, on not finding `.increment`, makes sure to check up in `functionStore` where it would find it.

We can make a link between these with `Object.create()`

```js
const user1 = Object.create(functionStore)
user1 // {}

user1. increment //function...
```

Interpreter doesn't find `.increment` on `user1` and looks up the prototype chain to the next object and finds `increment` 1 level up.

Solution in full

```js
function userCreator(name, score) {
    const newUser = Object.create(userFunctionStore);
    newUser.name = name;
    newUser.score = score;
    return newUser;
}

const userFunctionStore = {
    increment: function() { this.score++ },
    login: function() { console.log("You're logged in"); }
};

const user1 = userCreator("Phil", 4);
const user2 = userCreator("Eva", 5);
user1.increment();
```

The goal of OO is "Can we bundle up our relevent data and functionality". That is the fundamental goal.

## Prototype Walkthrough

Objects have a hidden property `__proto__` which in this example will link to the `userFunctionStore` object. This is a hidden reference. It doesn't mean we are copying `userFunctionStore` to our objects, it means we are _linking_ to it.

This is what's referred to as JavaScripts "prototypal nature". There are various keywords that automate creating this bond. Which we will cover later.

## Prototype Chain

![prototype-chain](/img/02-prototype-chain.png)

### Problem

No problems! It's beautiful

Maybe this is a little long-winded however.

```js
const newUser = Object.create(functionStore);
...
return newUser
```

Write this every single time - bit it's 6 words!

Super sophisticated but not standard.

## new & this Keywords

Introducing the keyword that automates the hard work: `new`

```js
const user1 = new userCreator("Phil", 4);
```

When we call the constructor function with `new` in fron we automate two things.

1. Create a new user object
2. return the new user object

But now we need to adjust how we write the body of userCreator - how can we:

* Refer to the auto-created object?
* Know where to put our single copies of functions?

No need to declare an object using object.create and no need to return it. It's going to do it automatically. Now however we need to adjust the body of the creator. How are we going to refer to the object we are assigning those properties to? The answer is `this`.

There is another challenge. As the object is being made automatically, how do we link things with `__proto__`? As we want to save ourselves making this bond, how do we do this?

## Function are Objects & Functions

Interlude—function are both objects and functions :/

```js
function multiplyBy2(num) {
    return num*2
}

multiplyBy2.stored = 5;
multiplyBy2(3) //6

multiplyBy2.stored // 5
multiplyBy2.prototype // {}
```

We could use the fact that all functions have a default property on their object veriosn, 'prototype', which is itself an object—to replace our functionStore object.

## new Keyword & Share Functions with prototype

```js
function UserCreator(name, score) {
    this.name = name;
    this.score = score;
}

UserCreator.prototype.increment = function () {
    this.score++;
};

UserCreator.prototype.login = function() {
    console.log("login");
}

const user1 = new UserCreator("Eva", 9);

user1.increment();
```

So here we are simplifying the creation and return of the initial object. We are also attaching some functions to the prototype of our object so that these functions will be linked to in each object instance that we create.

When we use new the folloing happens:

1. An object is created with a `this` context
2. a `__proto__` link is created to this new object
3. the object is returned

## Review of new

Using new is faster to write. 99% of developers don't know what's happening under the hood. We have to upper case first letter of the function so that we know it requires `new` to work.
