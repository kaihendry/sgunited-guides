# Arrow functions

ES6 arrow functions give us several benefits over ES5 functions:

- shorter syntax
- they allow `this` to follow the lexical scope rule (more about lexical scope later)

```js
const add = (x, y) => x + y;
```

## Tips

Implicit return. if you have a single line arrow function, you can remove the curly brackets and return statement, and it will work just the same.

Example of a simple callback to return an array with each element multiplied by 2:

```js
// ES5
[1, 2, 3].map(function (element) {
  return element * 2;
});

// ES6
[1, 2, 3].map((element) => {
  return element * 2;
});

// ES6 (optional curly braces removed + implicit return)
[1, 2, 3].map((element) => element * 2);
```

To implicitly return object literals, you need to surround the object's braces ({}) with brackets(()). This is because `{}` can mean a block and also a JavaScript object.

Example:

```js
// bad. won't work
["a", "b", "c"].map((alphabet, index) => {
  alphabet: index;
});

// good. will return the object as we expected
["a", "b", "c"].map((alphabet, index) => ({ alphabet: index }));
```

You don't need brackets (()) when there is only one argument to the function.
Brackets (()) are needed when your function has one of the following:

- multiple arguments
- no arguments
- rest parameters
- default parameters
- destructuring argument

## Arrow function vs ordinary function

Arrow functions do not have their own `this` value. The value of `this` inside an arrow function is always inherited from the enclosing scope.

### Context

- "this" keyword refers to the the context (where the code has reference to)
- the global "outermost" context, the global object in browser is the "window" object

```js
console.log(this === window); // true
```

Arrow function is the **preferred syntax** to declare a function in modern JavaScript because it allows `this` to follow the Lexical Scope rule.

Lexical Scope: functions are executed using the scope chain that was in effect when they were defined

```js
this.hello = "hello from out of wrapper";

function normalFn() {
  console.log("normal: ", this.hello);
}

const arrowFn = () => {
  console.log("arrow: ", this.hello);
};

function wrapper() {
  this.hello = "hello from wrapper";
  normalFn();
  arrowFn();
}

wrapper();
```

As you might observe, in a non-arrow function, `this` is passed into the function. Whereas in arrow function, `this` is using the context where is defined (lexical scope).

## When to use arrow functions?

You should follow these rules:

- Use non-arrow functions for methods that will be called using the object.method() syntax. Those are the functions that will receive a meaningful `this` value from their caller.
- Use arrow functions for everything else.

Further reading:

- https://medium.com/better-programming/3-examples-of-when-not-to-use-javascript-arrow-functions-90eebfbf7bb0

## References

- [Mozilla hacks: arrow functions](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)

## Exercises

https://github.com/thoughtworks-jumpstart/learning-functions/blob/master/lab3.js
