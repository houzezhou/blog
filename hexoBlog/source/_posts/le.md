---
title: 乐视答题
categories: 前端
tags: 
    - 前端
    - JS
#description: 
#date: 
---

曾经答题
<!-- more -->

###### 1、请在横线处补充代码，使代码按预期输出
```
function a(arg1, arg2) {
    console.log(arg1, arg2);
}
function b() {
    var args = [].slice.call(arguments, -2);
    a.apply(null, args);
}
b(2, 3, 1); // 输出：3 1
b(2, 3, 1, 5, 7); // 输出：5 7
b(2, 3, 1, 5, 7, 8); // 输出：7 8
```


###### 2、请在横线处补充代码，使代码按预期输出
```
function a() {
    return this + 1;
}
// 将调用参数分别加1
function b() {
    var i = 0, len = arguments.length, item;
    for (; i < len; i++) {
        item = a.call(arguments[i]);
        console.log(item);
    }
}
b(2, 0); // 输出：3 1
b(3, 5, 7); // 输出：4 6 8
```

###### 3、请问以下代码输出什么？
```
function noop() {
	
}
noop.name = 'op', noop.xxx = 'foo', noop.length = 1;
function fn(a, b) {
	
}
console.log(noop.name, noop.xxx, noop.length, fn.length);
// noop foo 0 2
```

###### 4、请问以下代码输出什么？
```
var a = 0, b = 2, x;
var c = (3, x);
console.log(a, b, c); // 0 2 undefined
```

###### 5、实现函数a，使代码按预期输出
// 如果str以下划线加数字结尾，则将最后的数字加1
// 否则给str加上`_1`
```
function a(str) {
    var res = str.replace(/_(\d+)$/, function (m, n) {
        return '_' + (1 + parseInt(n));
    });
    res === str && (res += '_1');

    console.log(res);
}
a('baidu'); // 输出：baidu_1
a('baidu_1'); // 输出：baidu_2
a('baidu_40'); // 输出：baidu_41
a('baidu_100_1'); // 输出：baidu_100_2
a('360'); // 输出：360_1
a('360_2'); // 输出：360_3
```

###### 6、请优化以下代码：
```
function exec() {
    // code
}
exec();
setInterval(exec, 100);

// 优化后
function exec() {
    // code
    setTimeout(exec, 100);
}
exec();
```

###### 7、实现简单的bind函数：
```
function bind(fn, context) {
    return function () {
        return fn.apply(context, arguments);
    };
}

//上面那个其实不对，应该如下： ---by 猴哥
// 参考地址： https://muyiy.cn/blog/3/3.4.html#%E6%A8%A1%E6%8B%9F%E5%AE%9E%E7%8E%B0
Function.prototype.myBind = function(context){
    // this指向调用者，这里保存调用者
    var self = this 

    // 如果用户处了 context 还传了其它参数，如 fun.myBind(Obj, bala1, bala2, bala3...)
    // 需要在这获取一下其它参数 ： bala1、bala2、bala3
    // 因为第一个参数是context对象，所以只截取这个参数之后的其它参数
    args = Array.prototype.slice.call(arguments, 1) 
    
    return function() {
        // 里面函数的 arguements 对象是指 myBind 执行完后返回的函数的参数对象
        var inArgs = Array.prototype.slice.call(arguements)
        return self.apply(context, args.concat(inArgs))
    }
}
// 这样算是在 Function 的原型上添加了myBind，所有的方法都可以  fun.myBind(obj, a, b, c...) 其中 a b c 是参数
```
```
// 测试用例如下：
var value = 2;

var foo = {
    value: 1
};

function bar(name, age) {
    return {
        value: this.value,
        name: name,
        age: age
    }
};

var bindFoo = bar.myBind(foo, "Jack");
bindFoo(20);
// {value: 1, name: "Jack", age: 20}
```

###### 8、代码如下，请问点击第3个li时控制台输出什么？
```
<ul>
  <li> index = 0 </li>
  <li> index = 1 </li>
  <li> index = 2 </li>
  <li> index = 3 </li>
</ul>
<script type="text/javascript">
    var nodes = document.getElementsByTagName('li');
    for (var i = 0; i < nodes.length; i++) {
        nodes[i].onclick = function () {
            console.log(i);
        };
    }
</script>
// 输出 4
```

###### 9、以下为遍历一个数组或对象的函数，并在某种条件下停止遍历。
handler为处理每个数组元素或对象里每个值的函数，请设计完成此each函数。
```
function each(obj, handler) {
    var i;
    if (obj instanceof Array) {
        i = 0;
        for (var len = obj.length; i < len; i++) {
            if (handler(obj[i], i) === false) {
                break;
            }
        }
    } else {
        for (i in obj) {
            if (obj.hasOwnProperty(i)) {
                if (handler(obj[i], i) === false){
                    break;
                }
            }
        }
    }
}
```

###### 10、写一个函数，实现把指定字符串重复指定次数，例如重复“ab”3次返回“ababab”。
```
function repeat(str, times) {
    if (times<1) {return ''}

    var res = '';
    while (times--) {
        res += str;
    }
    return res;
}
```


#### 第二套题

```
一、以下15题为所有人必答题

1、阅读以下代码，d、e、f的值分别是什么？
var a = 1, b = true, c = 3;
var d = a && b && c;
var e = a && b || c;
var f = a || b && c;

2、阅读以下代码，d、e、f的值分别是什么？
var a = 0, b = 2, c;
var d = a && b && c;
var e = a && b || c;
var f = a || b && c;

3、请优化以下代码：
var info = {
    b: typeof a != 'undefined' && a.startPage.b || '-',
    c: typeof a != 'undefined' && a.startPage.c || '-',
    d: typeof a != 'undefined' && a.startPage.d || false
};

4、请将b中的英文字符串全部替换成a对象里对应key的值，并将所有在a里找不到替换值的转换为大写。即替换后是：'今天是2017年04月02日（2017-04-02）。GOOD LUCK!';
var a = {
    YYYY: '2017',
    MM: '04',
    DD: '02'
};
var b = '今天是YYYY年MM月DD日（YYYY-MM-DD）。Good luck!';
b.replace(/\b[YMD]+\b/g,function($0){return a[$0]}).toUpperCase();
5、请将a转换成b：
var a = 'a: 1, b: 2, c: 3';
var b = 'a=1&b=2&c=3';

6、下列语句分别返回什么？
/ab/.test('abc');
/a\b/.test('abc');

7、var a = [1, 2, 3], b = [0];
用一个语句实现将数组a添加到数组b末尾，即使得 b = [0, 1, 2, 3]
注意，不要使用concat方法。（提示：用到apply）

b.push.apply(b,a);

8、优化以下代码：
var length = $('.js_uid') && $('.js_uid').length;
while (length) {
    // some code
    length = length - 1;
}

9、下面的代码是否有问题，如果有，是什么问题？
var hrefStr = window.location.href||'';
if (hrefStr) {
    if (hrefStr.indexOf('sso.le.com')!==-1) {
        return;
    }
}

10、请优化以下代码：
function urlChange(url){
    if(/le.com/.test(location.hostname)){
        return url.replace(/letv.com/,'le.com');
    }
    return url;
}

11、下面的代码是否有问题，如果有，是什么问题？
location.href = 'http://sso.le.com/User/sysCookie?userkey=' +
	user.userkey + '&next_action=' + location.href;

12、下面的代码如何改进？
var html = '<ul>'+
    '<li><a href="http://'+LETV.CONSTANT.host.SSO_LETV_COM+'/oauth/sina">新浪微博登录</a></b></li>'+
    '<li><a href="http://'+LETV.CONSTANT.host.SSO_LETV_COM+'/oauth/qq">QQ登录</a></b></li>'+
    '<li><a href="http://'+LETV.CONSTANT.host.SSO_LETV_COM+'">乐视网登录</a></b></li>'+
'</ul>';

13、var a = [1, 2, 10, 11, 4];
请调用数组的一个方法将a变成 [1, 2, 3, 4];

14、以下HTTP状态码分别代表什么？
200、301、302、304、400、404、500、502、504

15、说说GET请求与POST请求的区别。


二、以下为Node开发的同学要答的题

16、下面的代码是否有问题，如果有，是什么问题？
var res = yield cache.get('/cmsBlock:'+blockId+':'+newlang);
if (!res) {
    var result = yield request(geo.getCmsUrl(blockId)+'&lang='+newlang);
    res = yield formatData(result, block);
}
cache.set('/cmsBlock:'+blockId+':'+newlang, res, 2);

17、如何捕获Node异步调用抛出的异常？
18、如何捕获Koa中间件运行时抛出的异常？
19、Linux系统添加定时任务的命令是哪两个？
20、实现Node进程开机自启的PM2命令是什么？
21、location /tv { ... }
以上nginx路由是否能匹配“/tv/pin”、“/tvb/”？
22、location ~ ^/tv/?$ { ... }
以上nginx路由是否能匹配“/tv/pin”、“/izt/tv/”？
```


