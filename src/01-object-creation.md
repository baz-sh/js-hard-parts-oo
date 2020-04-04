# Object Creation

## Creating an object

Objects-store functions with their associated data!

```js
const user1 = {
    name: "Phil",
    score: 4,
    increment: function() {
        user.score++;
    }
};

user1.increment(); // user1.score => 4
```

This is the principle of encapsulation.

## Object dot Notations

What alternative techniques are there for creating objects?

```js
// user 'dot notation'
const user2 = {};

user2.name = "Julia"; // assign properties to that object
user2.score = 5;
user2.increment = function() {
    user2.score++;
};
```

## Object.create

Using `Object.create`.

```js
const user3 = Object.create(null);

user3.name = "Eva";
user3.score = 9;
user3.increment = function() {
    user3.score++;
};
```

## Creating Objects with Functions

You can also generate objects using a function.

```js
function userCreator(name, score) {
    const newUser = {};
    newUser.name = name;
    newUser.score = score;
    newUser.increment = function () {
        newUser.score++;
    };
    return newUser;
}

const user1 = userCreator("Phil", 4);
const user2 = userCreator("Julia", 5);
user1.increment();
```

