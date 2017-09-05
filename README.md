# Essentials-in-JavaScript-ES6

ECMAScript (ES) is a scripting language specification standardized by ECMAScript International. It is used by applications to enable client-side scripting. Languages like JavaScript, JScript and ActionScript are governed by this specification. I created this repo for the better understanding of the ES6 implementation in JavaScript.

## 1-3 Variables and scoping

ES6 provides two new ways of declaring variables: let and const, which mostly replace the ES5 way of declaring variables, var.

**let**

let works similarly to var, but the variable it declares is block-scoped, it only exists within the current block. var is function-scoped.

In the following code, you can see that the let-declared variable tmp only exists inside the block that starts in line A:
```
function order(x, y) {
    if (x > y) { // (A)
        let tmp = x;
        x = y;
        y = tmp;
    }
    console.log(tmp===x); // ReferenceError: tmp is not defined
    return [x, y];
}
```

**const**

const works like let, but the variable you declare must be immediately initialized, with a value that can’t be changed afterwards.
```
const foo;
    // SyntaxError: missing = in const declaration

const bar = 123;
bar = 456;
    // TypeError: `bar` is read-only
```
Since for-of creates one binding (storage space for a variable) per loop iteration, it is OK to const-declare the loop variable:
```
for (const x of ['a', 'b']) {
    console.log(x);
}
// Output:
// a
// b
```

Both let and const create variables that are block-scoped – they only exist within the innermost block that surrounds them. The following code demonstrates that the const-declared variable tmp only exists inside the block of the if statement:
```
function func() {
    if (true) {
        const tmp = 123;
    }
    console.log(tmp); // ReferenceError: tmp is not defined
}
```

In contrast, var-declared variables are function-scoped:
```
function func() {
    if (true) {
        var tmp = 123;
    }
    console.log(tmp); // 123
}
```

Block scoping means that you can shadow variables within a function:
```
function func() {
  const foo = 5;
  if (···) {
     const foo = 10; // shadows outer `foo`
     console.log(foo); // 10
  }
  console.log(foo); // 5
```

## 4-6 Destructuring

Destructuring is a convenient way of extracting multiple values from data stored in (possibly nested) objects and Arrays. It can be used in locations that receive data (such as the left-hand side of an assignment). How to extract the values is specified via patterns (read on for examples).

**Object destructuring**
```
const obj = { first: 'Jane', last: 'Doe' };
const {first: f, last: l} = obj;
    // f = 'Jane'; l = 'Doe'

// {prop} is short for {prop: prop}
const {first, last} = obj;
    // first = 'Jane'; last = 'Doe'
```

**Array destructuring**

Array destructuring (works for all iterable values):
```
const iterable = ['a', 'b'];
const [x, y] = iterable;
    // x = 'a'; y = 'b'
```

Destructuring helps with processing return values:
```
const [all, year, month, day] =
    /^(\d\d\d\d)-(\d\d)-(\d\d)$/
    .exec('2999-12-31');
```

## 7-8 Arrow functions

The “fat” arrow => (as opposed to the thin arrow ->) was chosen to be compatible with CoffeeScript, whose fat arrow functions are very similar.

Specifying parameters:
```
    () => { ... } // no parameter
     x => { ... } // one parameter, an identifier
(x, y) => { ... } // several parameters
```

Specifying a body:
```
x => { return x * x }  // block
x => x * x  // expression, equivalent to previous line
```

The statement block behaves like a normal function body. For example, you need return to give back a value. With an expression body, the expression is always implicitly returned.

Note how much an arrow function with an expression body can reduce verbosity. Compare:
```
const squares = [1, 2, 3].map(function (x) { return x * x });
const squares = [1, 2, 3].map(x => x * x);
```

## 9 Filter method

filter() method creates a new array with all elements that pass the test implemented by the provided function.

### Syntax
```
array.filter(callback[, thisObject]); 
```

```
function isBigEnough(element, index, array) { 
   return (element >= 10); 
} 
var passed = [12, 5, 8, 130, 44].filter(isBigEnough); 
console.log("Test Value : " + passed );  
```

## 10 Map method

Map is a key/value data structure in ES6. It provides a better data structure to be used for hash-maps. 
```
var map = new Map()
map.set('contra', { description: 'Asynchronous flow control' })
map.set('dragula', { description: 'Drag and drop' })
map.set('woofmark', { description: 'Markdown and WYSIWYG editor' })
```

One of the important differences is also that you’re able to use anything for the keys. You’re not just limited to primitive values like symbols, numbers, or strings, but you can even use functions, objects and dates – too. Keys won’t be casted to strings like with regular objects, either.
```
var map = new Map()
map.set(new Date(), function today () {})
map.set(() => 'key', { pony: 'foo' })
map.set(Symbol('items'), [1, 2])
```
