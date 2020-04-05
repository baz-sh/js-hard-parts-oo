# Scope & this

## Calling Prototype Methods

`this` in JS will appkly to the object that a funciton or method is called on. When we see `user1.increment` immediately in the execution context, `this` within `incrememnt` will bind to `user1`. It binds to the left of the '.'

When we invoked `.increment` on `user20` we look on the object for increment and don't find it. We look at the `__proto__` property and find it on the `UserCreator` object. We grab that code and in the execution context, we invoke it with the context of `user20` that is to say `this` is bound to `user20` and therefore increments `user20`'s score property.

## this Keyword Scoping Issues

what if we want to organize our code inside one of our shared functions - perhaps be defining a new inner function.

```js
function UserCreator(name, score) {
    this.name = name;
    this.score = score;
}

UserCreator.prototype.increment = function() {
    function add1() {
        this.score ++;
    }
    add1();
}

var user1 = new UserCreator("Eva", 9);
user1.increment();
```

In this code, there is no assignment to the left of add1. Therefore add1 gets invoked with the context of this being the global memory. Score will be undefined.

The solution to this problem is to introduce an arrow function. THis will bind it's `this` lexically.

```js
function UserCreator(name, score) {
    this.name = name;
    this.score = score;
}

UserCreator.prototype.increment = function() {
    const add1 = () => { this.score++ }
    add1();
}

var user1 = new UserCreator("Eva", 9);
user1.increment();
```

Being lexically scoped means that it will automatically refer to the `this` from where it was born.

## Solving Scope with Arrow Functions

Arrow functions are lexically scoped.

"Where I am on the page determines something about me when I get called". i.e. my scope / `this`.

## ES6 Class Keyword

The class acts as syntactic sugar over using the prototype object.

We're writing our shared methods seperately from our objects 'constructor' itself (off in the `User.prototype` object)

Other languages let us do this all in one place. ES2015 lets us do so too.

```js
class UserCreator {
    constructor(name, score) {
        this.name = name;
        this.score = score;
    }
    increment() {
        this.score++;
    }
    login() {
        console.log("Logged in");
    }
}

const user1 = new UserCreator("Eva", 9);
user1.increment();
```

## Recap of the class Keyword

The class keyword.

### Benefits

* Emerging as a new standard
* Feels more like style of other languages (e.g. Python)

### Problems

* 99% of developers have no idea how it works
