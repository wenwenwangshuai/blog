# JS简写骚操作

-----

## 三元操作符

使用三元操作符可以让你的`if...else`多行语句变成一行

**简化前：**

```js
const x = 20;
let answer;

if (x > 10) {
    answer = "greater than 10";
} else {
    answer =  "less than 10";
}
```

**简化后：**

```js
const answer = x > 10 ? "greater than 10" : "less than 10";
```

## 短路操作符

当进行变量赋值的时候，你可能需要确保被用来赋值的变量不是`null`、`undefined`或者为`空`。

**简化前：**

```js
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     let variable2 = variable1;
}
```

**简化后：**

```js
const variable2 = variable1  || 'new';
```

是不是感觉难以置信😢，试一试下面的代码：

```js
let variable1;
let variable2 = variable1  || 'bar';
console.log(variable2 === 'bar'); // prints true

variable1 = 'foo';
variable2 = variable1  || 'bar';
console.log(variable2); // prints foo
```

需要注意的是，如果 `varibale1` 的值为 `false` 或者是 `0` ，则 `'bar'` 将会被赋值给 `varibale2`.

## 声明变量

**简化前：**

```js
let x;
let y;
let z = 3;
```

**简化后：**

```js
let x, y, z=3;
```

## if判断是否存在

**简化前：**

```js
let a;
if ( a !== true ) {
// do something...
}
```

**简化后：**

```js
let a;
if ( !a ) {
// do something...
}
```

## for 循环

**简化前：**

```js
const fruits = ['mango', 'peach', 'banana'];
for (let i = 0; i < fruits.length; i++)
```

**简化后：**

```js
for (let fruit of fruits)
```

如果你想得到数组元素的下标，你可以这样子写：

```js
for (let index in fruits)
```

当你用这种方法获取对象的key时仍然有效

```js
const obj = {continent: 'Africa', country: 'Kenya', city: 'Nairobi'}
for (let key in obj)
  console.log(key) // output: continent, country, city
```

## 十进制指数

当需要写数字带有很多零时（如10000000），可以采用指数（1e7）来代替这个数字

**简化前：**

```js
for (let i = 0; i < 10000; i++) {}
```

**简化后：**

```js
for (let i = 0; i < 1e7; i++) {}

// 下面都是返回true
1e0 === 1;
1e1 === 10;
1e2 === 100;
1e3 === 1000;
1e4 === 10000;
1e5 === 100000;
```

## 对象属性

**简化前：**

```js
const x = 1920, y = 1080;
const obj = { x:x, y:y };
```

**简化后：**

```js
const obj = { x, y };
```

## return

**简化前：**

```js
function calcCircumference(diameter) {
  return Math.PI * diameter
}
```

**简化后：**

```js
calcCircumference = diameter => (
  Math.PI * diameter;
)
```

## 参数是默认值

**简化前：**

```js
function volume(l, w, h) {
  if (w === undefined)
    w = 3;
  if (h === undefined)
    h = 4;
  return l * w * h;
}
```

**简化后：**

```js
volume = (l, w = 3, h = 4 ) => (l * w * h);

volume(2) //output: 24
```

## 模板文本

**简化前：**

```js
const welcome = 'You have logged in as ' + first + ' ' + last + '.'

const db = 'http://' + host + ':' + port + '/' + database;
```

**简化后：**

```js
const welcome = `You have logged in as ${first} ${last}`;

const db = `http://${host}:${port}/${database}`;
```

## 解构赋值

**简化前：**

```js
const observable = require('mobx/observable');
const action = require('mobx/action');
const runInAction = require('mobx/runInAction');

const store = this.props.store;
const form = this.props.form;
const loading = this.props.loading;
const errors = this.props.errors;
const entity = this.props.entity;
```

**简化后：**

```js
import { observable, action, runInAction } from 'mobx';

const { store, form, loading, errors, entity } = this.props;
```

你甚至可以在解构的同时对变量重新命名：

```js
const { store, form, loading, errors, entity:contact } = this.props;
```

## "..."运算符

**简化前：**

```js
// joining arrays
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = arr.slice()
```

**简化后：**

```js
// joining arrays
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```

你还可以使用 `...` 运算符在一个数组的任意位置去嵌入另一个数组：

```js
const odd = [1, 3, 5 ];
const nums = [2, ...odd, 4 , 6];
```

`...` 和 `es6` 的解构赋值一起使用也很强大

```js
const { a, b, ...z } = { a: 1, b: 2, c: 3, d: 4 };
console.log(a) // 1
console.log(b) // 2
console.log(z) // { c: 3, d: 4 }
```

## 强制参数简写

JavaScript中如果没有向函数参数传递值，则参数为undefined。为了增强参数赋值，可以使用if语句来抛出异常，或使用强制参数简写方法。

**简写前：**

```js
function foo(bar) {
  if(bar === undefined) {
    throw new Error('Missing parameter!');
  }
  return bar;
}
```

**简写后：**

```js
mandatory = () => {
  throw new Error('Missing parameter!');
}

foo = (bar = mandatory()) => {
  return bar;
}
```

## 双重非位运算

有一个有效用例用于双重非运算操作符。可以用来代替Math.floor()，其优势在于运行更快，可以阅读此文章了解更多位运算。

**简写前：**

```js
Math.floor(4.9) === 4 //true
```

**简写后：**

```js
~~4.9 === 4 //true
```

## Array.find

**简化前：**

```js
const pets = [
  { type: 'Dog', name: 'Max'},
  { type: 'Cat', name: 'Karl'},
  { type: 'Dog', name: 'Tommy'},
]

function findDog(name) {
  for(let i = 0; i<pets.length; ++i) {
    if(pets[i].type === 'Dog' && pets[i].name === name) {
      return pets[i];
    }
  }
}
```

**简化后：**

```js
pet = pets.find(pet => pet.type ==='Dog' && pet.name === 'Tommy');
console.log(pet); // { type: 'Dog', name: 'Tommy' }
```

## 指数幂

**简化前：**

```js
Math.pow(2,3); // 8
Math.pow(2,2); // 4
Math.pow(4,3); // 64
```

**简写后：**

```js
2**3 // 8
2**4 // 4
4**3 // 64
```

## 字符串转数字

**简化前：**

```js
const num1 = parseInt("100");
const num2 =  parseFloat("100.01");
```

**简化后：**

```js
const num1 = +"100"; // converts to int data type
const num2 =  +"100.01"; // converts to float data type
```

## Object 深拷贝

```js
const obj = {a: 1,b: 2}
const obj2 = JSON.parse(JSON.stringify({ a:1 }));
```

## Object.entries()

这是一个 `es8` 中出现的特性，允许你把一个对象转换成具有键值对的数组。

```js
const credits = { producer: 'John', director: 'Jane', assistant: 'Peter' };
const arr = Object.entries(credits);
console.log(arr);

/** Output:
[ [ 'producer', 'John' ],
  [ 'director', 'Jane' ],
  [ 'assistant', 'Peter' ]
]
**/
```

## Object.values()

`Object.values()` 同样是 `es8` 里面出现的一个新特性，它和 `Object.entries()` 功能类似，但是在最终的转换数组中没有 `key`。

```js
const credits = { producer: 'John', director: 'Jane', assistant: 'Peter' };
const arr = Object.values(credits);
console.log(arr);

/** Output:
[ 'John', 'Jane', 'Peter' ]
**/
```

> 告诫自己，即使再累也不要忘记学习，成功没有捷径可走，只有一步接着一步走下去。 共勉！
