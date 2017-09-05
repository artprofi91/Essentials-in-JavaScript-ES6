# Essentials-in-JavaScript-ES6

ECMAScript (ES) is a scripting language specification standardized by ECMAScript International. It is used by applications to enable client-side scripting. Languages like JavaScript, JScript and ActionScript are governed by this specification. I created this repo for the better understanding of the ES6 implementation in JavaScript.

## 1-3 Variables and scoping

ES6 provides two new ways of declaring variables: let and const, which mostly replace the ES5 way of declaring variables, var.

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

