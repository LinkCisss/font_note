# font_note
前端的笔记
#前端进阶笔记

##一.JavaScript基础
> ###掘金部分

###1. 变量和类型√
1. JavaScript规定了几种语言类型
2. JavaScript对象的底层数据结构是什么
3. Symbol类型在实际开发中的应用、可手动实现一个简单的Symbol
4. JavaScript中的变量在内存中的具体存储形式
5. 基本类型对应的内置对象，以及他们之间的装箱拆箱操作
6. 理解值类型和引用类型
7. null和undefined的区别
8. 至少可以说出三种判断JavaScript数方式，以及他们的优缺点，如何准确的判断数组类型
9. 可能发生隐式类型转换的场景以及转换原则，应如何避免或巧妙应用
10. 出现小数精度丢失的原因，JavaScript可以存储的最大数字、最大安全数字，JavaScript处理大数字的方法、避免精度丢失的方法

### 2. 原型和原型链√
1. 理解原型设计模式以及JavaScript中的原型规则
2. instanceof的底层实现原理，手动实现一个instanceof
3. 实现继承的几种方式以及他们的优缺点

>###### 3.1 原型继承 √
``` JavaScript
function Parent1() {
    this.name = ['super1']
    this.reName = function () {
    this.name.push('super111')
  }
}
function Child1() {
}
Child1.prototype = new Parent1()
var child11 = new Child1()
var child12 = new Child1()
var parent1 = new Parent1()
child11.reName()
console.log(child11.name, child12.name) // [ 'super1', 'super111' ] [ 'super1', 'super111' ], 可以看到子类的实例属性皆来自于父类的一个实例，即子类共享了同一个实例
console.log(child11.reName === child12.reName) // true, 共享了父类的方法
```

>###### 3.2 构造函数继承 √
```JavaScript
function Child2() {
  Parent1.call(this)
}
var child21 = new Child2()
var child22 = new Child2()
child21.reName()
console.log(child21.name, child22.name) // [ 'super1', 'super111' ] [ 'super1' ], 子实例的属性都是相互独立的
console.log(child21.reName === child22.reName) // false, 实例方法也是独立的，没有共享同一个方法
```

>###### 3.3 组合继承 √
```
function Parent3() {
  this.name = ['super3']
}
Parent3.prototype.reName = function() {
  this.name.push('super31')
}
function Child3() {
  Parent3.call(this) // 生成子类的实例属性(但是不包括父对象的方法)
}
Child3.prototype = new Parent3() // 继承父类的属性和方法(副作用: 父类的构造函数被调用的多次，且属性也存在两份造成了内存浪费)
var child31 = new Child3()
var child32 = new Child3()
child31.reName()
console.log(child31.name, child32.name) // [ 'super3', 'super31' ] [ 'super3' ], 子类实例不会相互影响
console.log(child31.reName === child32.reName) //true, 共享了父类的方法
```

>###### 3.4 寄生继承
```
function Parent4() {
  this.name = ['super4']
}
Parent4.prototype.reName = function() {
  this.name.push('super41')
}
function Child4() {
  Parent4.call(this) // 生成子类的实例属性(但是不包括父对象的方法)
}
Child4.prototype = Object.create(Parent4.prototype) // 该方法会使用指定的原型对象及其属性去创建一个新的对象
var child41 = new Child4()
var child42 = new Child4()
child41.reName()
console.log(child41.name, child42.name) //[ 'super4','super41' ] [ 'super4' ], 子类实例不会相互影响
console.log(child41.reName === child42.reName) //true, 共享了父类的方法
```

>###### 3.5 ES6 Class
```
class Parent5 {
  constructor() {
    this.name = ['super5']
  }
  reName() {
    this.name.push('new 5')
  }
}
class Child5 extends Parent5 {
  constructor() {
    super()
  }
}
var child51 = new Child5()
var child52 = new Child5()
child51.reName()
console.log(child51.name, child52.name) // [ 'super5', 'new 5' ], 子类实例不会相互影响
console.log(child51.reName === child52.reName) //true, 共享了父类的方法
```

4. 至少说出一种开源项目(如Node)中应用原型继承的案例
5. [可以描述new一个对象的详细过程，手动实现一个new操作符](https://juejin.cn/post/6844904128276070407)
6. 理解es6 class构造以及继承的底层实现原理

### 3. 作用域和闭包
1.  理解词法作用域和动态作用域
2. 理解JavaScript的作用域和作用域链
3. 理解JavaScript的执行上下文栈，可以应用堆栈信息快速定位问题
4. this的原理以及几种不同使用场景的取值
5. 闭包的实现原理和作用，可以列举几个开发中闭包的实际应用
6. 理解堆栈溢出和内存泄漏的原理，如何防止
7. 如何处理循环的异步操作
8. 理解模块化解决的实际问题，可列举几个模块化方案并理解其中原理

>执行机制

1. 为何try里面放return，finally还会执行，理解其内部机制
2. JavaScript如何实现异步编程，可以详细描述EventLoop机制
3. 宏任务和微任务分别有哪些
4. 可以快速分析一个复杂的异步嵌套逻辑，并掌握分析方法
5. 使用Promise实现串行
6. Node与浏览器EventLoop的差异
7. 如何在保证页面运行流畅的情况下处理海量数据

#### 4. 语法和API
1. 理解ECMAScript和JavaScript的关系
2. 熟练运用es5、es6提供的语法规范，
3. 熟练掌握JavaScript提供的全局对象（例如Date、Math）、全局函数（例如decodeURI、isNaN）、全局属性（例如Infinity、undefined）
4. 熟练应用map、reduce、filter 等高阶函数解决问题
5. setInterval需要注意的点，使用settimeout实现setInterval
6. JavaScript提供的正则表达式API、可以使用正则表达式（邮箱校验、URL解析、去重等）解决常见问题
7. JavaScript异常处理的方式，统一的异常处理方案

<br/>
> ### github 问题部分

#### 1. 常见的浏览器内核有哪些 ？
* Trident 内核：IE, 360，搜狗浏览器 MaxThon、TT、The World,等。[又称 MSHTML]
* Gecko 内核：火狐，FF，MozillaSuite / SeaMonkey 等
* Presto 内核：Opera7 及以上。[Opera 内核原为：Presto，现为：Blink]
* Webkit 内核：Safari，Chrome 等。 [ Chrome 的：Blink（WebKit 的分支）]

***

#### 2. try/catch 无法捕获 promise.reject 的问题
[try..catch 结构，它只能是同步的，无法用于异步代码模式。](https://segmentfault.com/q/1010000014905440)

***

#### 3. [error 事件的事件处理程序](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalEventHandlers/onerror)

***

#### 4. 一个简易版的 Function.prototype.bind 实现

```  javascript
Function.prototype.bind = function (context) {
    var self = this;
    return function () {
        return self.apply(context, arguments);
    };
};

var obj = {
    name: '前端架构师'
};
var func = function () {
    console.log(this.name);
}.bind(obj);
func();
```
* [JavaScript】Function.prototype.bind 实现原理](https://blog.csdn.net/w390058785/article/details/83185847)

---

#### 5. call、apply、bind

>question

1. 怎么利用 call、apply 来求一个数组中最大或者最小值 ?
2. 如何利用 call、apply 来做继承 ?
3. apply、call、bind 的区别和主要应用场景 ?

>answer

* call 跟 apply 的用法几乎一样，唯一的不同就是传递的参数不同，call 只能一个参数一个参数的传入。
* apply 则只支持传入一个数组，哪怕是一个参数也要是数组形式。最终调用函数时候这个数组会拆成一个个参数分别传入。
* 至于 bind 方法，他是直接改变这个函数的 this 指向并且返回一个新的函数，之后再次调用这个函数的时候 this 都是指向 bind 绑定的第一个参数。
* bind 传参方式跟 call 方法一致。



还没写完


