# Default Prototype Chain

## Objects default __proto__

JavaScript uses this _proto_ link to give objects, functions and arrays a bunch of bonus functionality. All objects by defaul have `__proto__`.

```js
const obj = {
    num: 3
}

obj.num //3
obj.hasOwnProperty("num") // ? Where's this method?

Object.prototype // {hasOwnProperty: FUNCTION}
```

* With `Object.create` we override the default `__proto__` reference to `Object.prototype` and replace with `functionStore`
* But functionStore is an object so _it_ has a `__proto__` reference to `Object.prototype`—we just intercede in the chain.

## Function.prototype and Array.prototype

Arrays and functions are also object so they get access to all the functions in `Object.prototype` but also more goodies

```js
function multiplyBy2(num) {
    return num*2
}

multiplyBy2.toString(); //where is this method?

Function.prototype // { toString: FUNCTION, call: FUNCTION, bind: FUNCTION}

multiplyBy2.hasOwnProperty("score") //where is this function?

Function.prototype.__proto__ // Object.prototype { hasOwnProperty: FUNCTION}
```

What's meant by the 'pototype chain' is when JS can't find a method, it looks at the objects proto reference and tries to find it there. If it can't, it looks at that objects proto reference and so on.
