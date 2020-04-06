# Subclassing with new and call

## Create an Object with new

By using `new` an object will automatically be created in a new execution context and the `__proto__` will be linked to `this` (the objects prototype) and it will also be returned.

```js
function userCreator(name, score) {
    this.name = name;
    this.score = score;
}

userCreator.prototype.sayName = function() {
    console.log(`Hi, I'm ${this.name}`);
}

const user1 = new userCreator("Phil", 5);
// inside new, object created, proto linked and object also returned for "free".
```

![object-new](/img/06-obj-new.png)

## Creating a Subclass with a Constructor



## Using a call Method in a Constructor

## Assigning Properties to Instance

## Prototype tracing