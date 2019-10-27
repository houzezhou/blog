---
title: Okcoin-滴滴-贝壳
categories: 前端
tags: 
    - 前端
    - JS
#description: 
#date: 
---

面试，2019年，记录下来
<!-- more -->
####  贝壳

###### 1、Promise.all() 返回什么？ 手动实现一个 Promise.all()？
待补充...
1. 利用promise手动实现promiseAll
https://juejin.im/post/5c3d702ee51d4551b747f0ac
```
function PromiseAll (arr) {
	//PromiseAll的返回值为一个promise对象
	return new Promise((resolve, reject) => {
		//PromiseAll的入参必须是函数
		if (!Array.isArray(arr)) {
			return reject(new TypeError('arr must be an array.'));
		}

		let resArr = [];

		for (let i in arr) {
			(function(i) {
				Promise.resolve(arr[i]).then(res => {
					resArr.push(res);
					//只有所有的都成功了，才会返回resolve
					if (i == arr.length - 1) {
						return resolve(resArr);
					}
				}, err => {
					return reject(err)
				}).catch(err => {
					console.log(err)
				})
			})(i)
		}
	})
}
```

###### 2、简述下事件模型？ jquery 的 $ on 同时在父元素上监听两个事件，一个本身事件，一个子元素的委托事件，点击子元素时，哪个先触发？
答案是每次都是 委托事件 先触发，不知道为什么，原生js的话，是谁先注册谁先触发（跟代码顺序有关，而jqery的 on 一直是 委托事件先触发）
```
<ul id='ul'>
    <li></li>
    <li></li>
</ul>

var ul = $('#ul');
ul.on('click', function() {
    console.log('父元素本身事件 触发')
})
ul.on('click', 'li', function() {
    console.log('委托事件 触发')
})
```

###### 3、react 源码目录结构有哪些？react 有哪几个模块？
###### 4、 阻止事件冒泡  e.stopPropagation()

#### 滴滴

###### 1、 函数参数是值传递（执行时，实参是copy了一份，开辟了一个新的空间，存了起来，不是直接传的原参数）
如果参数是原始类型，直接一个全新的值，如果一个对象类型，也是一个全新的引用地址，不过此时新的引用和旧的引用都指向原对象

```
var m = {a: 11}
function foo(m) {
    m = {b: 22}  // 此时是把新的引用地址指向了新的对象，而原来的引用地址还是指向 {a: 11},并且原对象没修改
}
foo(m)
console.log(m) // => {a: 11}
```
```
var m = {a: 11}
function foo(m) {
    m.b = 22
}
foo(m)
console.log(m) // => {a: 11, b: 22}
```
###### 2、 call()、apply()、bind(),有什么不同，参数都有哪些？手动实现一个bind()  函数

###### 3、去掉字符串两端的空格， str.trim()、正则
```
去除字符串内所有的空格：str = str.replace(/\s*/g,"");
去除字符串内左侧的空格：str = str.replace(/^\s*/,"");
去除字符串内右侧的空格：str = str.replace(/(\s*$)/g,"");
去除字符串内两头的空格：str = str.replace(/^\s*|\s*$/g,"");
```

###### 4、 event.target 和 event.currentTarget 分别是是什么？有什么区别？
event.target：触发事件的元素   li
event.currentTarget：绑定事件处理程序的元素  ul
一般是同一个元素，事件委托时，不一样

###### 5、如何判断字符串是否两端对称？

###### 6、一个字符串里有大括号，小括号，如何判断所有的括号是 合法对称的？

#### OkCoin

###### 1、sessionStorage 和 localStorage 有啥区别？
sessionStorage 浏览器tab关掉时，就消失了，localStorage 还存在
待补充
...

###### 2、 fun.bind(obj) 返回的 function == fun 吗？

#### 58

###### 1、 a = [1,2,3,4]  b=[1,2,3,4]  a+b=?
###### 2、 a = [1,2,3,4]      1 + a = ?
###### 3、 1-[1] = ？
###### 4、 css怎样实现内容只有一行的时候居中显示，多行的时候居左显示

#### 伴鱼口语

###### 1、请写出你了解的Array方法，至少6个，哪些改变原数组，哪些不改变生成新数组？
push splice filter map forEach sort reduce
###### 2、写出输出结果
```
console.log(1)
async function foo(){
	console.log(2)
	await console.log(3)
	console.log(4)
}
setTimeout(function(){
	console.log(5)
},0)
foo()
new Promise(function(resolve,reject){
	console.log(6)
	resolve()
}).then(function(){
	console.log(7)
})
console.log(8)

// => 1 2 3 6 8 4 7 5
// await 立马执行，await所在function里 await 后面的代码，相当与放到了回调 Promise.then() 里面，不知道这理解对不对？
```
###### 3、写出输出结果
```
var name = 'The Window'
function func(){
	console.log(this.name)
}
var object ={
	name: 'MY Object',
	getNameFunc: function(fn){
		fn && fn();
		return function() {
			return this.name 
		}
	}
}

console.log(object.getNameFunc(func)())
// => The Window
// => The Window
```
###### 4、写出输出结果
```
let obj = {a: 0}
function fun(obj){
    obj.a = 1         // 新老引用都指向外层对象 {a: 0}，通过新引用修改也影响外层
    obj = {a: 2}      // 新的引用指向了新的对象，和老的对象脱离了关系
    obj.b = 2         // 修改新的对象
}
fun(obj)
concole.log(obj)

// 函数参数是值传递，copy了一份引用，不是外层的 obj
// =>  {a: 1}
```

###### 5、 输入 [2,0,2,1,1,0] 返回 [0,0,1,1,2,2]
实现一个方法，不能使用排序函数如 sort、reverse，要原地排序，不能申请多余的存储空间

###### 6、实现一个 lazyMan
实现一个LazyMan，可以按照以下方式调用:
LazyMan(“Hank”)输出:
Hi! This is Hank!

LazyMan(“Hank”).sleep(10).eat(“dinner”)输出
Hi! This is Hank!
//等待10秒..
Wake up after 10
Eat dinner~

LazyMan(“Hank”).eat(“dinner”).eat(“supper”)输出
Hi This is Hank!
Eat dinner~
Eat supper~

LazyMan(“Hank”).sleepFirst(5).eat(“supper”)输出
//等待5秒
Wake up after 5
Hi This is Hank!
Eat supper
以此类推。
复

作者：子非
链接：https://juejin.im/post/5c7f7051f265da2dbf5f2e64
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
+ ES6 方式：
```
class _LazyMan {
  constructor(name) {
    this.tasks = [];
    const task = () => {
      console.log(`Hi! This is ${name}`);
      this.next();
    }
    this.tasks.push(task);
    setTimeout(() => {               // 把 this.next() 放到调用栈清空之后执行
      this.next();
    }, 0);
  }

  next() {
    const task = this.tasks.shift(); // 取第一个任务执行
    task && task();
  }

  sleep(time) {
    this._sleepWrapper(time, false);
    return this;                     // 链式调用
  }

  sleepFirst(time) {
    this._sleepWrapper(time, true);
    return this;
  }

  _sleepWrapper(time, first) {
    const task = () => {
      setTimeout(() => {
        console.log(`Wake up after ${time}`);
        this.next();
      }, time * 1000)
    }
    if (first) {
      this.tasks.unshift(task);     // 放到任务队列顶部
    } else {
      this.tasks.push(task);        // 放到任务队列尾部
    }
  }

  eat(name) {
    const task = () => {
      console.log(`Eat ${name}`);
      this.next();
    }
    this.tasks.push(task);
    return this;
  }
}

function LazyMan(name) {
  return new _LazyMan(name);
}

```
+ ES5 方式：
这是典型的JavaScript流程控制，问题的关键是如何实现任务的顺序执行。在Express有一个类似的东西叫中间件，这个中间件和我们这里的吃饭、睡觉等任务很类似，每一个中间件执行完成后会调用next()函数，这个函数用来调用下一个中间件。

对于这个问题，我们也可以利用相似的思路来解决，首先创建一个任务队列，然后利用next()函数来控制任务的顺序执行：
[知乎链接](https://zhuanlan.zhihu.com/p/22387417)
```
function _LazyMan(name) {
    this.tasks = [];   
    var self = this;

    var fn =(function(n){
        var name = n;
        return function(){
            console.log("Hi! This is " + name + "!");
            self.next();
        }
    })(name);
    this.tasks.push(fn);
    setTimeout(function(){
        self.next();
    }, 0); // 在下一个事件循环启动任务
}

/* 事件调度函数 */
_LazyMan.prototype.next = function() { 
    var fn = this.tasks.shift();
    fn && fn();
}

_LazyMan.prototype.eat = function(name) {
    var self = this;
    var fn =(function(name){
        return function(){
            console.log("Eat " + name + "~");
            self.next()
        }
    })(name);
    this.tasks.push(fn);
    return this; // 实现链式调用
}

_LazyMan.prototype.sleep = function(time) {
    var self = this;
    var fn = (function(time){
        return function() {
            setTimeout(function(){
                console.log("Wake up after " + time + "s!");
                self.next();
            }, time * 1000);
        }
    })(time);
    this.tasks.push(fn);
   return this;
}

_LazyMan.prototype.sleepFirst = function(time) {
    var self = this;
    var fn = (function(time) {
        return function() {
            setTimeout(function() {
                console.log("Wake up after " + time + "s!");
                self.next();
            }, time * 1000);
        }
    })(time);

    this.tasks.unshift(fn);
    return this;
}

/* 封装 */
function LazyMan(name){
    return new _LazyMan(name);
}
```

