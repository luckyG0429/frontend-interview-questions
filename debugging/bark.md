## Original code

```js
function Dog(name) {
  this.name = name
}
Dog.bark = function() {
  console.log(this.name + ' says woof')
}
let fido = new Dog('fido')
fido.bark()
```

## Corrected code

```js
function Dog(name) {
  this.name = name
}
Dog.prototype.bark = function() {
  console.log(this.name + ' says woof')
}
let fido = new Dog('fido')
fido.bark()
```

## Explanation

When you `new` a function in JavaScript, it creates a new object whose methods are inherited from the `prototype` of the function you `new`'d. This is called prototypal inheritance. Defining something on the prototype vs. on the function directly is analogous to defining something as an instance property vs. as a static property on a `class`.

在JavaScript中，当你使用关键词new一个函数事，它会创建一个新的对象，这个对象同时会继承来自你的new的构造函数圆形上的一些方法。这个成为原型继承。在原型上定义跟在构造函数本身上直接定义，这就好比，你在一个实例属性上定义 跟 你在一个类上添加静态方法。

This code incorrectly defined `bark` directly on `Dog`. So when you `new` a `Dog`, the resulting object won't inherit the `bark` property. For it to inherit `bark`, we need to move `bark` to `Dog`'s `prototype`.

这段代码错误是因为直接在Dog的构造函数上定义了bark方法。所以当你实例化一个Dog对象时，该对象并不会继承bark属性。想要让它继承bark属性，我们需要把bark函数添加到Dog的原型链上。

