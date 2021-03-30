# Math及其常用的方法

----

### Math数学函数，但是它属于对象类型的

```js
typeof Math => "object"
```

之所以叫做数学函数，是因为Math这个对象中提供了很多操作数字的方法

### Math中提供的方法

**`abs()`: 取绝对值**

```js
Math.abs(10); // 10
Math.abs(-10); // 10
```

**`ceil()`/`floor()`: 向上/向下取整**

```js
Math.ceil(10); // 10
Math.ceil(10.01); // 11
Math.ceil(-10.01); // -10

Math.floor(10); // 10
Math.floor(10.01); // 10
Math.floor(-10.01); // -11
```

**`round()`: 四舍五入**

```js
Math.round(10.49); // 10
Math.round(10.5); // 11
Math.round(-10.49); // -10
Math.round(-10.5); // -10 此处要注意
Math.round(-10.51); // -11
```

注意：round()方法的话会将括号内的数`+0.5`之后，`向下取值`

**`max()`/`min()`: 取最大值/最小值**

```js
Math.max(13,14,520); // 520
Math.min(13,14,520); // 13
```

**`sqrt()`: 开平方**

```js
Math.sqrt(100); // 10
Math.sqrt(10); // 3.1622776601683795
Math.sqrt(16); // 4
```

**`pow(N,M)`: 取幂（N的M次方）**

```js
Math.pow(2,10); // 1024
```

**`PI`: 获取圆周率**

```js
Math.PI; // 3.141592653589793
```

**`random()`: 获取0-1之间的随机小数**

```js
for(let i = 0; i < 5; i++) {
  console.log(Math.random())
}
// 0.20241670856520422
// 0.5160179563129974
// 0.001590337430050548
// 0.9651583970501534
// 0.7426699741686391
```

**`Math.round(Math.random()*(m-n)+n)`: 获取n~m 之间的随机整数**

```js
for(let i = 0; i < 5; i++) {
  console.log(Math.round(Math.random()*(100-10)+10))
}
// 85
// 84
// 24
// 87
// 77
```
