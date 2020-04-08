# Subclassing with class, extends & super

## Create an Object with a Class

ES205 class approach.

```js
class userCreator {
    constructor(name, score) {
        this.name = name;
        this.score = score;
    }
    sayName() {
        console.log(`I am ${this.name}`);
    }
    increment() {
        this.score++;
    }
}

const user1 = new userCreator("Phil", 4);
const user2 = new userCreator("Tim", 4);

user1.sayName();

class paidUserCreator extends userCreator {
    constructor(paidName, paidScore, accountBalance) {
        super(paidName, paidScore);
        this.accountBalance = accountBalance;
    }
    increaseBalance() {
        this.accountBalance++;
    }
}

const paidUser1 = new paidUserCreator("Alyssa", 8, 25);
paidUser1.increaseBalance();
paidUser1.sayName();
```
