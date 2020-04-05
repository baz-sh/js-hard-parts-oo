# Sublassing with Factory Functions

## Subclassing and Inheritance

A core aspect of an OOP approach is inheritance - passking knoweldge down.

![inheritance](/img/05-inheritance.png)

## Create object with Factory Function

Factory function approach to subclassing.

```js
// the initial user
function userCreator(name, score) {
    const newUser = {};
    newUser.name = name;
    newUser.score = score.
    return newUser;
}

// the initial functions
userFunctions = {
    sayName: function() {
        console.log(`I'm ${this.name}`);
    }
    increment: function() {
        this.score++;
    }
}

const user1 = userCreator("Phil", 5);
user1.sayName(); // I'm Phil

// the paid user
function paidUserCreator(paidName, paidScore, accountBalance) {
    const newPaidUser = userCreator(paidName, paidScore);
    // link the paidUser to the paid user functions
    Object.setPrototypeOf(newPaidUser, paidUserFunctions);
    newPaidUser.accountBalance = accountBalance;
    return newPaidUser
}

// the paid user functions
const paidUserFunctions = {
    increaseBalance : function() {
        this.accountBalance++;
    }
};

// link the paid user functions to the user functions
Object.setPrototypeOf(paidUserFunctions, userFunctions);

const paidUser1 = paidUserCreator("Alyssa", 8, 25);
paidUser1.increaseBalance(); // 26
paidUser1.sayName(); // I'm Alyssa
```

## Create a Sub-Factory Function

The "magic" in the above code comes from `Object.setPrototypeOf`. The first argument is the object you want to set the `__proto__` reference of, and the second argument is what you want it to be. `Object.setPrototypeOf(newPaidUser, paidUserFunctions);` says "Set the `__proto__` link of newPaidUser to be paidUserFunctions".

## Subclass Review

### Interlude

We have another way of running a function that allow us to control the assignment of this.

```js
const obj = {
    num : 3,
    increment: function {this.num++}
};

const otherObj = {
    num: 10
};

obj.increment() // obj.num now 4
obj.inrement.call(otherObj) // otherObj.num now 11
```

`this` always refers to the object to the left of the dot on which the function is being called—unless we override that by running the function using `.call()` or `.apply()` which lets us set the value of `this` inside of the `increment` function.

## Call and Apply

