# 易错知识点

## 1、for...of 仅作用于拥有迭代器的对象

### 迭代器

* 拥有迭代器的对象我们叫做 `iterable` ，而迭代器叫做 `iterator` ，这是两个不同的概念
* 所有拥有 `[Symbol.iterator]()` 的对象被称为可迭代的
* 原理：
  
  `for-of` 循环首先调用集合的 `[Symbol.iterator]()` 方法，紧接着返回一个新的迭代器对象。迭代器对象可以是任意具有 `next()` 方法的对象； `for-of` 循环将重复调用这个方法，每次循环调用一次

### 原理及实现

1. 给对象添加一个名称为 Symbol.iterator 的属性方法。Symbol.iterator 是一个内置符号，代表一个迭代器方法。
2. Symbol.iterator 这个方法必须返回一个迭代器对象，包含一个 next 方法

> `next()` 方法每次执行都返回一个结果对象，这个对象有两个属性：
> * `value` ，表示将要返回的值；
> * `done` ，是一个布尔值，表示是否进行下次迭代

3. 迭代器还会保存一个 内部指针 ，用来指向当前集合中值的位置，每调用一次 next() 方法，都会返回下一个可用的结果对象。

```js
var obj = { a: 1, b: 2 };

Object.prototype[Symbol.iterator] = function () {
    const keys = Object.keys(this);
    let index = 0;

    return {
        next: () => {
            return {
                value: this[keys[index++]], // 每次迭代的结果
                done: index > keys.length // 迭代结束标识 false停止迭代，true继续迭代
            };
        }
    }
}

for (let n of obj) {
    console.log(n);
    /**
     * 1
     * 2
     */
}
```