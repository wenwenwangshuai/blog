# 前端常用的string函数方法！！

## 1、通过字符串函数获取字符串指定位置字符

---

### 1.1 charAt()

> 从某个字符串取得具体的字符，如果index的位置不在字符串中则返回空字符串

```js
let str = 'JsCoding';
// 语法
demo.charAt(index)
// demo
str.charAt(3)   =>  'o'
```

### 1.2 charCodeAt()

> 和`chartAt()`用法类似，只不过返回的是字符串的Unicode。同理，如果index下标不在字符串中，则返回空。

```js
let str = 'JsCoding';
// 语法
demo.charCodeAt(index)
// demo
str.charCodeAt(3)   =>  '111'
```

## 2、通过字符串函数对字符串的样式进行改变

---

### 2.1 big

> 将字符串字号变大，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.big()
```

### 2.2 small

> 将字符串字号变小，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.small()
```

### 2.3 bold

> 将字符串字体加粗，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.bold()
```

### 2.4 italics

> 将字符串设为斜体，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.italics()
```

### 2.5 blink

> 将字符串设为闪动，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.blink()
```

### 2.6 fixed

> 将字符串以打印机文本显示，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.fixed()
```

### 2.7 strike

> 将字符串加上删除线，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.strike()
```

### 2.8 fontcolor

> 设置字符串指定颜色，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.fontcolor('Blue')
```

### 2.9 fontsize

> 设置字符串指定字号，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.fontsize(22)
```

### 2.10 toLowerCase

> 将字符串转化为小写，并返回新的字符串。

```js
let txt = "JINGDIANYOUMEIJUZU"
txt.toLowerCase()
```

### 2.11 toUpperCase

> 将字符串转化为大写，并返回新的字符串。

```js
let txt = "jingdianyoumeijuzu"
txt.toUpperCase()
```

### 2.12 sub

> 将字符串显示为下标，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.sub()
```

### 2.13 sup

> 将字符串显示为上标，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.sup()
```

### 2.14 link

> 将字符串显示为链接，并返回新的字符串。

```js
let txt = "公众号：经典优美句子"
txt.link()
```

## 3、判断指定字符是否出现在字符串中，并返回其位置

---

### 3.1 indexOf()

> 判断指定字符首次出现在字符串中的位置，没有则返回-1。检查方式从前往末尾,下标0开始。

```js
let str = 'JsCoding';
// 语法 value => 指定字符，startindex => 指定位置开始
demo.indexOf(value,startindex)
// demo
str.indexOf('s')   =>  1
str.indexOf('s', 3)   =>  -1
```

### 3.2 lastIndexOf()

> 判断指定字符最后一次出现在字符串中的位置，没有则返回-1，检查方式为从末尾往前。如果指定的value值在指定位置之前，则返回的是最后一个出现value的位置。

```js
let str = 'JsCoding';
// 语法 value => 指定字符，startindex => 指定位置开始
demo.lastIndexOf(value,startindex)
// demo
str.lastIndexOf('s')   =>  1
str.lastIndexOf('s', 3)   =>  1
```

**注意：indexOf() 和 lastIndexOf() 都区分大小写。**

## 4、对字符串进行操作

---

### 4.1 replace()

> 用于字符串中以指定字符替换指定字符。

```js
let str = 'JsCoding';
// 语法 regexp/substr => 需要替换的文本或正则对象，replaceText => 替换的文本
demo.replace(regexp/substr,replaceText)
// demo
str.replace(/JsCoding/, 'JsCoding：是执行上下文的微信号')   
// 结果 => 
"JsCoding：是执行上下文的微信号"
```

### 4.2 slice()

> 获取字符串中的某个部分，并返回获取的部分。

```js
let str = 'JsCoding';
// 语法 start => 起始位置，end => 结束位置
demot.slice(start,end)
// demo
str.slice(1,3)   
// 结果 => 
"sC"
```

### 4.3 substr()

> 获取字符串从指定位置开始，指定长度的字符。

```js
let str = 'JsCoding';
// 语法 start => 起始位置，length => 长度
demo.substr(start,length)
// demo
str.substr(1,3)   
// 结果 => 
"sCo"
```

### 4.4 substring()

> 获取字符串指定区间的字符。

```js
let str = 'JsCoding';
// 语法 start => 起始位置必须为存在的下标，end => 结束位置可以为负数，则往前寻找。
demo.substring(start,end)
// demo
str.substring(1,3)   
// 结果 => 
"sC"

str.substring(3,-3)   
// 结果 => 
"JsC"

如果start === end 则返回空。
```

### 4.5 split()

> 将字符串分割成字符串数组。

```js
let str = 'JsCoding';
// 语法 separator => 字符串or表达式，howmany => 分割字符串的长度。
demo.split(separator,howmany)
// demo
str.split('' ,3)   
// 结果 => 
["J", "s", "C"]

str.split('')   
// 结果 => 
["J", "s", "C", "o", "d", "i", "n", "g"]
```

### 4.6 match()

> 返回所有查找的关键字内容的数组。

```js
let str = 'JsCoding';
let reg = /di/ig;

// 语法 searchvalue => 检索的字符串值，regexp => 匹配的RegExp对象。
demo.match(searchvalue or  RegExp)
// demo
str.match(reg)
// 结果 => 
["di"]

str.match('di')   
// 结果 => 
["di"]
```

**注意：String 对象的方法 slice()、substring() 和 substr() （不建议使用）都可返回字符串的指定部分。slice() 比 substring() 要灵活一些，因为它允许使用负数作为参数。slice() 与 substr() 有所不同，因为它用两个字符的位置来指定子串，而 substr() 则用字符位置和长度来指定子串。**

## 5、其他

---

### anchor()

> 用来创建HTML锚

```js
let text = '执行上下文'
text.anchor('前端公众号')

// 结果：
<a name="前端公众号">执行上下文</a>
```

## 6、日常小用途

---

### 6.1 将 'Coding, Js' => 'Js Coding'

```js
var str = "Coding, Js";
str.replace(/(\w+)\s*, \s*(\w+)/, "$2 $1");

// 结果

"Js Coding"
```

### 6.2 将双引号变成单引号

```js
var str = '"Js", "Coding"'
str.replace(/"([^"]*)"/g, "'$1'");

// 结果

"'Js', 'Coding'"
```

### 6.3 将字符串第一个字母改为大写

```js
var str = 'jjj sss ccc';
zhuan = str.replace(/\b\w+\b/g, function(c){
  return c.substring(0,1).toUpperCase() + c.substring(1);}
)

// 结果

"Jjj Sss Ccc"
```

### 6.4 将字符串中指定字符替换成指定字符

```js
var str = 'ccadjlkj3kajgl2lkjalg'
str.replace(/d/, '"公众号：经典优美句子"')

// 结果

"cca"公众号：经典优美句子"jlkj3kajgl2lkjalg"
```
