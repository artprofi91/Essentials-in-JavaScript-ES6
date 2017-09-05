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