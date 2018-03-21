## Original code

```js
for (var i = 0; i < 4; i++) {
  setTimeout(() => console.log(i), 0)
}
```

## Corrected code

```js
for (let i = 0; i < 4; i++) {
  setTimeout(() => console.log(i), 0)
}
```

## Explanation

There are two types of variable declarations in JavaScript: block-level declarations (using `let`, `const`, and in `catch` clauses), and function-level declarations (using `var`). Since this code uses `var`, it declares a single variable `i` that is shared by all four calls to `setTimeout`; by the time the first `setTimeout` is actually fired, the loop has already run four times and `i` equals `4`.

在JavaScript中有两种变量的声明方式：块级声明（使用let，const，和在catch的语句中），和 作用域声明（使用var定义）。在第一个代码块中使用var,声明了一个变量i，通过四次调用，i是被共享的。等到第一次调用settimeout的时候，循环已经完成了四次，所以i等于4

The fix is to make sure each call to `setTimeout` has its own instance of `i`, which doesn't change between the time when we set the timeout and the timeout is actually fired. There are a few ways we can do this:

为了确保每次调用setTimeout时有属于它自己的变量i的值，也就是说当我们每一次的调用，彼此之间不会被改变。我们可以通过这些方法实现：

1. Change `var` to `let`, which is a block-level declaration
1. 声明变量使用let而不是var， let是一个块级声明，仅在当前的代码块可使用
2. Pass `i` to `setTimeout` as its third argument, so `i` is passed in as the argument in `setTimeout`'s callback
2. 给setTimeout传递变量i的值作为函数的第三个参数，这样，变量i会作为一个参数被放在setTimeout的回调函数中
3. Wrap the `setTimeout` in an Immediately-Invoked-Function-Expression and pass `i` into it
3.利用立即执行函数表达式来包裹setTimeout函数，并把i作为参数穿进去，

I chose option 1 for its minimal code change, and positive effect on readability.
我选择第一种，因为它的代码改动极小，而且易于理解
