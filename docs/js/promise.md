# Promise的基本使用

---

## 含义

Promise是ES6新增的一个内置类，主要是用来管理异步编程的。
用`new Promise([executor])`创建一个Promise实例，需要传递一个可执行函数，此函数接收两个参数（函数类型：内部写好的两个函数，`resolve/reject`），内部会立即执行这个函数，返回一个Promise实例

一个Promise实例都会有以下：

* 内置私有属性（我们访问不到）
  * [[PromiseState]] 实例状态：`pending`准备状态，`fulfilled/resolved`成功状态，`rejected`失败状态
  * [[PromiseResult]] 实例的值

* 公共方法（Promise.prototype）
  * `then`
  * `catch`
  * `finally`

## 用法

```js
// 该bool用来帮助模拟成功或失败
let bool=false
// 封装Promise
let fn = () => {
  // 返回promise实例
  return new Promise((resolve,reject) => {
    if(bool) {
      // 成功执行resolve
      resolve('成功');
    } else {
      // 失败执行reject
      reject('失败');
     }
  })
}
// 注意，成功和失败的回调函数都只能接收一个参数
fn().then(data => console.log(data),error => console.log(error)) // "失败"
```

## API

### 1. Promise.resolve(result)

> 制造一个成功或失败

```js
Promise.resolve(1).then(value => console.log(value));
// 1

Promise.resolve(new Promise((resolve,reject) => reject('制造失败'))).then(null,error => console.log(error));
// 制造失败
```

### 2. Promise.reject(reason)

> 制造一个失败

```js
Promise.reject(2).then(value => console.log(value),error => console.log('失败'))
// 失败
```

### 3. Promise.all(array)

> 等待全部成功，或者有一个失败

```js
Promise.all([Promise.reject('err1'),Promise.resolve(1)]).then(value => console.log(value),error => console.log(error))
// err1

Promise.all([Promise.resolve(1),Promise.reject('err2')]).then(value => console.log(value),error => console.log(error))
// err2

Promise.all([Promise.resolve(1),Promise.resolve(2)]).then(value => console.log(value),error => console.log(error))
// [1,2]

Promise.all([Promise.reject('err3'),Promise.reject('err4')]).then(value => console.log(value),error => console.log(error))
// err3
```

### 4. Promise.race(array)

> 等待第一个状态改变

```js
Promise.race([Promise.reject('err1'),Promise.resolve(1)]).then(value=>console.log(value),error=>console.log(error))
// err1

Promise.race([Promise.resolve(1),Promise.reject('err2')]).then(value=>console.log(value),error=>console.log(error))
// 1

Promise.race([Promise.resolve(1),Promise.resolve(2)]).then(value=>console.log(value),error=>console.log(error))
// 1

Promise.race([Promise.reject('err3'),Promise.reject('err4')]).then(value=>console.log(value),error=>console.log(error))
// err3
```

### 5. Promise.allSettled(array)

> all只要有一个失败就中断，但我们希望拿到所有结果
> allSettled是等待全部promise状态改变

```js
Promise.allSettled([Promise.reject('err1'),Promise.resolve(1)]).then(value=>console.log(value),error=>console.log(error))
// [{reason: "err1",status: "rejected"},{status: "fulfilled",value: 1}]

// 自己模拟实现Promise.allSettled
Promise.allSettled2 = (promiseList) => {
    return Promise.all(promiseList.map(promise=>promise.then((value)=>{return {status:"ok",value}},(value)=>({status:"not ok",value}))))
}
```

### 手写Promise.all

```js
function all(promiseArray){
    return new Promise((resolve,reject)=>{
        if(!Array.isArray(promiseArray)){
            return reject(new Error('传入的参数必须是数组'));
        }
        let res=[];
        let counter=0;
        for(let i=0;i<promiseArray.length;i++){
            Promise.resolve(promiseArray[i]).then(value=>{
                counter++;
                res[i]=value;
                if(counter===promiseArray.length){
                    return resolve(res);
                }
            }).catch(
                e=>{
                    reject(new Error('失败'));
                }
            )
        }
    })
}

var promise1 = Promise.resolve(3);
var promise2 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});
var promise3 = 42;

all([promise1, promise2, promise3]).then(function(values) {
  console.log(values);
});
```

### 手写Promise.race

```js
function race(promiseArray){
    return new Promise((resolve,reject)=>{
        if(!Array.isArray(promiseArray)){
            return reject(new Error('传入的参数必须是数组'));
        }
        for(let i=0;i<promiseArray.length;i++){
            Promise.resolve(promiseArray[i]).then(value=>{
                resolve(value)
            }).catch(
                e=>{
                    reject(new Error('失败'));
                }
            )
        }
    })
}

var promise1 = Promise.resolve(3);
var promise2 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});
var promise3 = 42;

race([promise1, promise2, promise3]).then(function(values) {
  console.log(values);
});
```
