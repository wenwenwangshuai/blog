# redux和vuex

vuex 和 redux 都是状态管理库，用于单独管理状态的。其中，redux是一个范用的库，可以单独使用。而vuex是专门用来配合vue使用的。他们都应用了flux架构的思想，但是在接口的提供上稍有不同。

## redux

----

redux这个库首先引入了以下的几个概念

1. state
2. reducer
3. action
4. dispatch

其中，state的作用是存储数据状态的，reducer的作用是根据指示对状态进行修改的，acticon的作用是描述某一次的状态应该如何修改的，dispatch的作用是驱动状态进行修改。

redux中提供了相应的api来实现这些功能，示例代码如下：

```js
import {createStore} from 'redux'
// 创建一个Store类的实例,传入reducer
const store = createStore(reducer);
// reducer就是一个函数，接收当前的状态和action，根据action的指示来修改状态
// reducer的返回值就是最新的状态
function reducer(state, action){
	// 根据action中type的值修改state，并返回
}
// 查看当前的状态
store.getState()
// 驱动状态发生改变
let action = {type: 'ADD', step: 1}
store.dispatch(action);
```

**当然redux中也引入了异步action的功能**

更多的情况下，我们的状态修改是要和异步请求结合在一起的。当然我们可以在异步请求成功后，再去修改状态，例如这样

```js
fetch('xxxxx').then(res => res.json).then(data => {
	store.dispatch({type:'INIT', data})
})
```

这样的方式固然可以通过状态管理库和异步请求相结合，但是组合性太差。

所以，我们使用redux本身提供的中间件就比较完美了。redux的中间可以这么理解，就是action可以被每个中间件依次处理，处理后返回新的action然后交给下一个中间件继续处理，每一个中间件都有自己的熔断机制（调用next(actioin)可以自行决定是否交给后续的中间件处理）。默认的dispatch可以被认为是默认的中间件（该中间件有触发reducer的能力）。不过，redux的中间件模式采用了柯里化的api风格，最后呈现给我们的是修改了原始的dispatch方法，使dispatch拥有更多的功能。

每层中间件都有固定的接口，可以看一下代码示例：

```js
import {createStore, applyMiddleware} from 'redux'

// 创建一个redux中间件,可以让dispatch接收函数 
function createMiddle(){
	// 返回的这个函数会作为中间件，其中
    // store表示仓库实例，可以获取state和dispatch等
    // next表示真正的dispatch
    // action表示的是上一个中间件返回的action
	return store => next => action => {
    	if(typeof action === 'function'){
        	action(next)
        }else{
        	next(action)
        }
    }
}

const store = createStore(reducer, appliMiddleware(createMiddle()));
// 触发的时候
let action = dispatch => {
	fetch('xxx').then(response => response.json()).then(data => {
    	dispatch({type: 'ADD', data});
    })
}
store.dispatch(action);
```

## vuex

---

vuex是专门来配合vuejs做状态管理的一个库，结合了vue数据响应的特点，同样的vuex中也引入了几个概念。

1. state
2. getters
3. mutations
4. actions

vuex对状态的管理大体是这样的，state中存储状态，getters是对state状态的一个衍生。而状态的改变都交给了mutations来处理，我们可以直接从视图中来驱动mutations，让状态发生变化。actions是用来处理异步的，当然在actions中也可以驱动mutations，来改变状态。

代码使用如下：

```js
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

const store = new Vuex.Store({
	state: {
    	sex: true // 表示性别
    },
    getters: {
    	showSex(state){
        	return state.sex ? '男' : '女' // 根据中状态衍生出显示的结果
        }
    },
    mutations: {
    	setSex(state, payload){
        	state.sex = payload.sex // 根据载荷去修改sex的值
        }
    },
    actions: {
    	getSexState(store){
        	fetch('xxx').then(response => response.json()).then(data => {
            	store.commit('setSex', {sex: data.sex});
            })
        }
    }
})

store.commit('setSex', {sex: false}); // 修改状态
store.dispatch('getSexState'); // 根据异步请求的结果修改状态
```
