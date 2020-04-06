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

```js
function userCreator(name, score) {
    this.name = name;
    this.score = score;
}

userCreator.prototype.sayName = function() {
    console.log(`Hi, I'm ${this.name}`);
}

userCreator.prototype.increment = function() {
    this.score++;
}

const user1 = new userCreator("Phil", 5);
const user2 = new userCreator("Tim", 4);

function paidUserCreator(paidName, paidScore, accountBalance) {
    userCreator.call(this, paidName, paidScore);
    this.accountBalance = accountBalance;
}

paudUserCreator.prototype = Object.create(userCreator.prototype);

paidUserCreator.prototype.increaseBalance = function() {
    this.accountBalance++;
}

const paidUser1 = new paidUserCreator("Alyssa", 8, 25);
paidUser1.increaseBalance()
paidUser1.sayName() // Hi, I'm Alyssa
```

This method would ovveride the prototype object and put a new one in there (using `Object.create`). This is an alternative to using `Object.setPrototypeOf`. Both methods are legitimate uses.

## Using a call Method in a Constructor

## Assigning Properties to Instance

## Prototype tracing