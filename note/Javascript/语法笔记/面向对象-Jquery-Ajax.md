#### 五.面向对象

- 首先，我们要明确，面向对象不是语法，是一个思想，是一种 **编程模式**
- 面向： 面（脸），向（朝着）
- 面向过程： 脸朝着过程 =》 关注着过程的编程模式
- 面向对象： 脸朝着对象 =》 关注着对象的编程模式
- 实现一个效果
  - 在面向过程的时候，我们要关注每一个元素，每一个元素之间的关系，顺序，。。。
  - 在面向过程的时候，我们要关注的就是找到一个对象来帮我做这个事情，我等待结果
- 我们以前的编程思想是，每一个功能，都按照需求一步一步的逐步完成



##### 创建对象的方式

- 因为面向对象就是一个找到对象的过程
- 所以我们先要了解如何创建一个对象



###### 调用系统内置的构造函数创建对象

- js 给我们内置了一个 Object 构造函数

- 这个构造函数就是用来创造对象的

- 当 构造函数 和 new 关键字连用的时候，就可以为我们创造出一个对象

- 因为 js 是一个动态的语言，那么我们就可以动态的向对象中添加成员了

  ```javascript
  // 就能得到一个空对象
  var o1 = new Object() 
  
  // 正常操作对象
  o1.name = 'Jack'
  o1.age = 18
  o1.gender = '男'
  ```



###### 字面量的方式创建一个对象

- 直接使用字面量的形式，也就是直接写 `{}`

- 可以在写的时候就添加好成员，也可以动态的添加

  ```javascript
  // 字面量方式创建对象
  var o1 = {
    name: 'Jack',
    age: 18,
    gender: '男'
  }
  
  // 再来一个
  var o2 = {}
  o2.name = 'Rose'
  o2.age = 20
  o2.gender = '女'
  ```



###### 使用工厂函数的方式创建对象

- 先书写一个工厂函数

- 这个工厂函数里面可以创造出一个对象，并且给对象添加一些属性，还能把对象返回

- 使用这个工厂函数创造对象

  ```javascript
  // 1. 先创建一个工厂函数
  function createObj() {
    // 手动创建一个对象
    var obj = new Object()
  
    // 手动的向对象中添加成员
    obj.name = 'Jack'
    obj.age = 18
    obj.gender = '男'
  
    // 手动返回一个对象
    return obj
  }
  
  // 2. 使用这个工厂函数创建对象
  var o1 = createObj()
  var o2 = createObj()
  ```

  

###### 使用自定义构造函数创建对象

- 工厂函数需要经历三个步骤

  - 手动创建对象
  - 手动添加成员
  - 手动返回对象

- 构造函数会比工厂函数简单一下

  - 自动创建对象
  - 手动添加成员
  - 自动返回对象

- 先书写一个构造函数

- 在构造函数内向对象添加一些成员

- 使用这个构造函数创造一个对象（和 new 连用）

- 构造函数可以创建对象，并且创建一个带有属性和方法的对象

- 面向对象就是要想办法找到一个有属性和方法的对象

- 面向对象就是我们自己制造 **构造函数** 的过程

  ```javascript
  // 1. 先创造一个构造函数
  function Person(name, gender) {
    this.age = 18
    this.name = name
    this.gender = gender
  }
  
  // 2. 使用构造函数创建对象
  var p1 = new Person('Jack', 'man')
  var p2 = new Person('Rose', 'woman')
  ```

  

##### 构造函数详解

- 我们了解了对象的创建方式
- 我们的面向对象就是要么能直接得到一个对象
- 要么就弄出一个能创造对象的东西，我们自己创造对象
- 我们的构造函数就能创造对象，所以接下来我们就详细聊聊 **构造函数**



###### 构造函数的基本使用

- 和普通函数一样，只不过 **调用的时候要和 new 连用**，不然就是一个普通函数调用

  ```javascript
  function Person() {}
  var o1 = new Person()  // 能得到一个空对象
  var o2 = Person()      // 什么也得不到，这个就是普通函数调用
  ```

  - 注意： **不写 new 的时候就是普通函数调用，没有创造对象的能力**

- 首字母大写

  ```javascript
  function person() {}
  var o1 = new person() // 能得到一个对象
  
  function Person() {}
  var o2 = new Person() // 能得到一个对象
  ```

  - 注意： **首字母不大写，只要和 new 连用，就有创造对象的能力**

- 当调用的时候如果不需要传递参数可以不写 `()`，建议都写上

  ```javascript
  function Person() {}
  var o1 = new Person()  // 能得到一个空对象
  var o2 = new Person    // 能得到一个空对象 
  ```

  - 注意： **如果不需要传递参数，那么可以不写 （），如果传递参数就必须写**

- 构造函数内部的 this，由于和 new 连用的关系，是指向当前实例对象的

  ```javascript
  function Person() {
    console.log(this)
  }
  var o1 = new Person()  // 本次调用的时候，this => o1
  var o2 = new Person()  // 本次调用的时候，this => o2
  ```

  - 注意： **每次 new 的时候，函数内部的 this 都是指向当前这次的实例化对象**

- 因为构造函数会自动返回一个对象，所以构造函数内部不要写 return

  - 你如果 return 一个基本数据类型，那么写了没有意义
  - 如果你 return 一个引用数据类型，那么构造函数本身的意义就没有了

  

###### 使用构造函数创建一个对象

- 我们在使用构造函数的时候，可以通过一些代码和内容来向当前的对象中添加一些内容

  ```javascript
  function Person() {
    this.name = 'Jack'
    this.age = 18
  }
  
  var o1 = new Person()
  var o2 = new Person()
  ```

  - 我们得到的两个对象里面都有自己的成员 **name** 和 **age**

- 我们在写构造函数的时候，是不是也可以添加一些方法进去呢？

  ```javascript
  function Person() {
    this.name = 'Jack'
    this.age = 18
    this.sayHi = function () {
      console.log('hello constructor')
    }
  }
  
  var o1 = new Person()
  var o2 = new Person()
  ```

  - 显然是可以的，我们的到的两个对象中都有 `sayHi` 这个函数
  - 也都可以正常调用

- 但是这样好不好呢？缺点在哪里？

  ```javascript
  function Person() {
    this.name = 'Jack'
    this.age = 18
    this.sayHi = function () {
      console.log('hello constructor')
    }
  }
  
  // 第一次 new 的时候， Person 这个函数要执行一遍
  // 执行一遍就会创造一个新的函数，并且把函数地址赋值给 this.sayHi
  var o1 = new Person()
  
  // 第二次 new 的时候， Person 这个函数要执行一遍
  // 执行一遍就会创造一个新的函数，并且把函数地址赋值给 this.sayHi
  var o2 = new Person()
  ```

  - 这样的话，那么我们两个对象内的 `sayHi` 函数就是一个代码一摸一样，功能一摸一样
  - 但是是两个空间函数，占用两个内存空间
  - 也就是说 `o1.sayHi` 是一个地址，`o2.sayHi` 是一个地址
  - 所以我们执行 `console.log(o1 === o2.sayHi)` 的到的结果是 `false`
  - 缺点： **一摸一样的函数出现了两次，占用了两个空间地址**

- 怎么解决这个问题呢？

  - 就需要用到一个东西，叫做 **原型**



##### 原型

- 原型的出现，就是为了解决 **构造函数的缺点**
- 也就是给我们提供了一个给对象添加函数的方法
- 不然构造函数只能给对象添加属性，不能合理的添加函数就太 LOW 了



###### prototype

- **每一个函数天生自带一个成员，叫做 prototype，是一个对象空间**

- 即然每一个函数都有，构造函数也是函数，构造函数也有这个对象空间

- 这个 `prototype` 对象空间可以由函数名来访问

  ```javascript
  function Person() {}
  
  console.log(Person.prototype) // 是一个对象
  ```

  - 即然是个对象，那么我们就可以向里面放入一些东西

  ```javascript
  function Person() {}
  
  Person.prototype.name = 'prototype'
  Person.prototype.sayHi = function () {}
  ```

- 我们发现了一个叫做 `prototype` 的空间是和函数有关联的

- 并且可以向里面存储一些东西

- 重点： **在函数的 prototype 里面存储的内容，不是给函数使用的，是给函数的每一个实例化对象使用的**

- 那实例化对象怎么使用能？



###### \_\_proto\_\_

- **每一个对象都天生自带一个成员，叫做 `__proto__`，是一个对象空间**

- 即然每一个对象都有，实例化对象也是对象，那么每一个实例化对象也有这个成员

- 这个 `__proto__` 对象空间是给每一个对象使用的

- 当你访问一个对象中的成员的时候

  - 如果这个对象自己本身有这个成员，那么就会直接给你结果
  - 如果没有，就会去 `__proto__` 这个对象空间里面找，里面有的话就给你结果
  - 未完待续。。。

- 那么这个 `__proto__` 又指向哪里呢？

  - 这个对象是由哪个构造函数 new 出来的
  - 那么这个对象的 `__proto__` 就指向这个构造函数的 `prototype`

  ```javascript
  function Person() {}
  
  var p1 = new Person()
  
  console.log(p1.__proto__ === Person.prototype) // true
  ```

  - 我们发现实例化对象的 `__proto__` 和所属的构造函数的 `prototype` 是一个对象空间
  - 我们可以通过构造函数名称来向 `prototype` 中添加成员
  - 对象在访问的时候自己没有，可以自动去自己的 `__proto__` 中查找
  - 那么，我们之前构造函数的缺点就可以解决了
    - 我们可以把函数放在构造函数的 `prototype` 中
    - 实例化对象访问的时候，自己没有，就会自动去 `__proto__` 中找
    - 那么也可以使用了

  ```javascript
  function Person() {}
  
  Person.prototype.sayHi = function () {
    console.log('hello Person')
  }
  
  var p1 = new Person()
  p1.sayHi()
  ```

  - `p1` 自己没有 `sayHi` 方法，就会去自己的 `__proto__` 中查找
  - `p1.__proto__` 就是 `Person.prototype`
  - 我们又向 `Person.prototype` 中添加了 `sayHi` 方法
  - 所以 `p1.sayHi` 就可以执行了

- 到这里，当我们实例化多个对象的时候，每个对象里面都没有方法

  - 都是去所属的构造函数的 `protottype` 中查找
  - 那么每一个对象使用的函数，其实都是同一个函数
  - 那么就解决了我们构造函数的缺点

  ```javascript
  function Person() {}
  
  Person.prototype.sayHi = function () {
    console.log('hello')
  }
  
  var p1 = new Person()
  var p2 = new Person()
  
  console.log(p1.sayHi === p2.sayHi)
  ```

  - `p1` 是 `Person` 的一个实例
  - `p2` 是 `Person` 的一个实例
  - 也就是说 `p1.__proto__` 和 `p2.__proto__` 指向的都是 `Person.prototype`
  - 当 `p1` 去调用 `sayHi` 方法的时候是去 `Person.prototype` 中找
  - 当 `p2` 去调用 `sayHi` 方法的时候是去 `Person.prototype` 中找
  - 那么两个实例化对象就是找到的一个方法，也是执行的一个方法

- 结论

  - 当我们写构造函数的时候
  - **属性我们直接写在构造函数体内**
  - **方法我们写在原型上**

tip:注意property与preopertype的区分

ECMAScript可以识别两种类型的对象，一种叫做Native Object属于语言范畴;一种叫做Host Object，由运行环境提供例如document对象，Dom Node等

Native objects是一种松散的结构并且可以动态的增加属性(property)，所有的属性都有一个名字和一个值，这个值可以是另一个对象的引用
或者是内建的数据类型(String, Number, Boolean, Null 或者 Undefined)
下面的这个简单的例子描述了一个[javascript](https://so.csdn.net/so/search?q=javascript&spm=1001.2101.3001.7020)对象是如何设置一个属性的值和如何读取属性的值的。







##### 原型链

- 我们刚才聊过构造函数了，也聊了原型
- 那么问题出现了，我们说构造函数的 `prototype` 是一个对象
- 又说了每一个对象都天生自带一个 `__proto__` 属性
- 那么 **构造函数的 prototype** 里面的 `__proto__` 属性又指向哪里呢？



###### 一个对象所属的构造函数

- 每一个对象都有一个自己所属的构造函数

- 比如： 数组

  ```javascript
  // 数组本身也是一个对象
  var arr = []
  var arr2 = new Array()
  ```

  - 以上两种方式都是创造一个数组
  - 我们就说数组所属的构造函数就是 `Array`

- 比如： 函数

  ```javascript
  // 函数本身也是一个对象
  var fn = function () {}
  var fun = new Function()
  ```

  - 以上两种方式都是创造一个函数
  - 我们就说函数所属的构造函数就是 `Function`



###### constructor

- 对象的 `__proto__` 里面也有一个成员叫做 **`constructor`**
- 这个属性就是指向当前这个对象所属的构造函数



###### 链状结构

- 当一个对象我们不知道准确的是谁构造的时候，我们呢就把它看成 `Object` 的实例化对象
- 也就是说，我们的 **构造函数 的 prototype 的 `__proto__`** 指向的是 `Object.prototype`
- 那么 `Object.prototype` 也是个对象，那么它的 `__proto__` 又指向谁呢？
- 因为 `Object` 的 js 中的顶级构造函数，我们有一句话叫 **万物皆对象**
- 所以 `Object.prototype` 就到顶了，`Object.prototype` 的 `__proto__` 就是 null



###### 原型链的访问原则

- 我们之前说过，访问一个对象的成员的时候，自己没有就会去 `__proto__` 中找
- 接下来就是，如果 `__proto__` 里面没有就再去 `__proto__` 里面找
- 一直找到 `Object.prototype` 里面都没有，那么就会返回 `undefiend`



###### 对象的赋值

- 到这里，我们就会觉得，如果是赋值的话，那么也会按照原型链的规则来
- 但是： **并不是！并不是！并不是！** 重要的事情说三遍
- 赋值的时候，就是直接给对象自己本身赋值
  - 如果原先有就是修改
  - 原先没有就是添加
  - 不会和 `__proto__` 有关系



##### ES5继承

###### 构造函数继承



```js
function person(name,age){
    this.name=name
    this.age=age
}
function Student(name,age,classroom){
            Person.call(this,name,age)
            this.classroom = classroom
}
//只继承了所有属性没有继承原型的函数（没有用new person创建，call只是调用了person）
```



###### 原型继承

```js
Student.prototype = new Person()
//new完以后的原型复制给student
```



###### 组合继承

构造函数继承+原型继承

```js
function Person(name,age){
    this.name = name
    this.age = age
}

Person.prototype.say = function(){
    console.log("hello")
}

function Student(name,age,classroom){
    Person.call(this,name,age)
    this.classroom = classroom
}

Student.prototype = new Person()

var obj = new Student("kerwin",100,"1班")
```

##### es6继承

```js
 <script>
        //父类
        class Person {
            constructor(name,age){
                this.name = name
                this.age = age
            }
            say(){
                console.log(this.name,"hello")
            }
        }
        //子类
        //extends 原型继承
        class Student extends Person{
            constructor(name,age,grade){
                super(name,age) // Person.call(this,name,age)
                this.grade = grade
            }

            say(){
                super.say() //语法糖
                console.log(this.name,"你好")
            }
        }

        var obj = new Student("kerwin",100,100)
        console.log(obj)
        obj.say()
    </script>
```







#### 六. AJAX

- `ajax` 全名 `async javascript and XML`
- 是前后台交互的能力
- **也就是我们客户端给服务端发送消息的工具，以及接受响应的工具**
- 是一个 **默认异步** 执行机制的功能



##### AJAX 的优势

1. 不需要插件的支持，原生 js 就可以使用
2. 用户体验好（不需要刷新页面就可以更新数据）
3. 减轻服务端和带宽的负担
4. 缺点： 搜索引擎的支持度不够，因为数据都不在页面上，搜索引擎搜索不到



##### AJAX 的使用

- 在 js 中有内置的构造函数来创建 ajax 对象
- 创建 ajax 对象以后，我们就使用 ajax 对象的方法去发送请求和接受响应



###### 创建一个 ajax 对象

```javascript
// IE9及以上
const xhr = new XMLHttpRequest()

// IE9以下
const xhr = new ActiveXObject('Mricosoft.XMLHTTP')
```

- 上面就是有了一个 ajax 对象
- 我们就可以使用这个 `xhr` 对象来发送 ajax 请求了



###### 配置链接信息

```javascript
const xhr = new XMLHttpRequest()

// xhr 对象中的 open 方法是来配置请求信息的
// 第一个参数是本次请求的请求方式 get / post / put / ...
// 第二个参数是本次请求的 url 
// 第三个参数是本次请求是否异步，默认 true 表示异步，false 表示同步
// xhr.open('请求方式', '请求地址', 是否异步)
xhr.open('get', './data.php')
```

- 上面的代码执行完毕以后，本次请求的基本配置信息就写完了



###### 发送请求

```javascript
const xhr = new XMLHttpRequest()
xhr.open('get', './data.php')

// 使用 xhr 对象中的 send 方法来发送请求
xhr.send()
```

- 上面代码是把配置好信息的 ajax 对象发送到服务端



###### 一个基本的 ajax 请求

- 一个最基本的 ajax 请求就是上面三步
- 但是光有上面的三个步骤，我们确实能把请求发送的到服务端
- 如果服务端正常的话，响应也能回到客户端
- 但是我们拿不到响应
- 如果想拿到响应，我们有两个前提条件
  1. 本次 HTTP 请求是成功的，也就是我们之前说的 http 状态码为 200 ~ 299
  2. ajax 对象也有自己的状态码，用来表示本次 ajax 请求中各个阶段



###### ajax 状态码

- ajax 状态码 - `xhr.readyState`
- 是用来表示一个 ajax 请求的全部过程中的某一个状态
  - `readyState === 0`：  表示未初始化完成，也就是 `open` 方法还没有执行
  - `readyState === 1`：  表示配置信息已经完成，也就是执行完 `open` 之后
  - `readyState === 2`：  表示 `send` 方法已经执行完成
  - `readyState === 3`：  表示正在解析响应内容
  - `readyState === 4`：  表示响应内容已经解析完毕，可以在客户端使用了
- 这个时候我们就会发现，当一个 ajax 请求的全部过程中，只有当 `readyState === 4` 的时候，我们才可以正常**使用**服务端给我们的数据
- 所以，配合 http 状态码为 200 ~ 299 
  - 一个 ajax 对象中有一个成员叫做 `xhr.status` 
  - 这个成员就是记录本次请求的 http 状态码的
- 两个条件都满足的时候，才是本次请求正常完成



###### readyStateChange

- 在 ajax 对象中有一个事件，叫做 `readyStateChange` 事件

- 这个事件是专门用来监听 ajax 对象的 `readyState` 值改变的的行为

- 也就是说只要 `readyState` 的值发生变化了，那么就会触发该事件

- 所以我们就在这个事件中来监听 ajax 的 `readyState` 是不是到 4 了

  ```javascript
  const xhr = new XMLHttpRequest()
  xhr.open('get', './data.php')
  
  xhr.send()
  
  xhr.onreadyStateChange = function () {
    // 每次 readyState 改变的时候都会触发该事件
    // 我们就在这里判断 readyState 的值是不是到 4
    // 并且 http 的状态码是不是 200 ~ 299
    if (xhr.readyState === 4 && /^2\d{2}$/.test(xhr.status)) {
      // 这里表示验证通过
      // 我们就可以获取服务端给我们响应的内容了
    }
  }
  ```

  

###### **xhr.onload**

```js
xhr.onload = function{
if(xhr.status===200){

 }
}
//只有readystatus=4的时候执行
```



###### responseText

- ajax 对象中的 `responseText` 成员

- 就是用来记录服务端给我们的响应体内容的

- 所以我们就用这个成员来获取响应体内容就可以

  ```javascript
  const xhr = new XMLHttpRequest()
  xhr.open('get', './data.php')
  
  xhr.send()
  
  xhr.onreadyStateChange = function () {
    if (xhr.readyState === 4 && /^2\d{2}$/.test(xhr.status)) {
      // 我们在这里直接打印 xhr.responseText 来查看服务端给我们返回的内容
      console.log(xhr.responseText)
    }
  }
  ```

  

##### 使用 ajax 发送请求时携带参数

- 我们使用 ajax 发送请求也是可以携带参数的
- 参数就是和后台交互的时候给他的一些信息
- 但是携带参数 get 和 post 两个方式还是有区别的



###### 发送一个带有参数的 get 请求

- get 请求的参数就直接在 url 后面进行拼接就可以

  ```javascript
  const xhr = new XMLHttpRequest()
  // 直接在地址后面加一个 ?，然后以 key=value 的形式传递
  // 两个数据之间以 & 分割
  xhr.open('get', './data.php?a=100&b=200')
  
  xhr.send()
  
  
          //ajax
          /*
              get 偏向获取数据
              post 偏向提交数据
              put 偏向更新（全部）{name:"kerwin",age:100}
              delete 偏向删除信息
  
              patch 偏向部分修改
  
              header
              options
              connnect
          */
  ```

  - 这样服务端就能接受到两个参数
  - 一个是 a，值是 100
  - 一个是 b，值是 200



###### 发送一个带有参数的 post 请求

- post 请求的参数是携带在请求体中的，所以不需要再 url 后面拼接

  ```javascript
  const xhr = new XMLHttpRequest()
  xhr.open('get', './data.php')
  
  // 如果是用 ajax 对象发送 post 请求，必须要先设置一下请求头中的 content-type
  // 告诉一下服务端我给你的是一个什么样子的数据格式
  xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded')
  
  // 请求体直接再 send 的时候写在 () 里面就行
  // 不需要问号，直接就是 'key=value&key=value' 的形式
  xhr.send('a=100&b=200')
  ```

  - `application/x-www-form-urlencoded` 表示的数据格式就是 `key=value&key=value`

    ```js
    xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded") //name=kerwin&age=100
    xhr.send(`username=shanzhen&password=456`)
    ```

  - json

  ```js
  xhr.setRequestHeader("Content-Type","application/json") 
  xhr.send(JSON.stringify({
                  username:"ximen",
                  password:"789"
              }))
  ```

  

###### json-server 

P139

-基于一个json文件就可以创建很多的后端模拟接口

json-server .\test.json --watch

##### 封装ajax✅

```js
/*
 * @作者: kerwin
 * @公众号: 大前端私房菜
 */
function queryStringify(obj) {
  let str = ''
  for (let k in obj) str += `${k}=${obj[k]}&`
  return str.slice(0, -1)
}

// 封装 ajax
function ajax(options) {
  let defaultoptions = {
    url: "",
    method: "GET",
    async: true,
    data: {},
    headers: {},
    success: function () { },
    error: function () { }
  }
  let { url, method, async, data, headers, success, error } = {
    ...defaultoptions,
    ...options
  }

  if (typeof data === 'object' && headers["content-type"]?.indexOf("json") > -1) {
    data = JSON.stringify(data)
  }
  else {
    data = queryStringify(data)

  }
  // 如果是 get 请求, 并且有参数, 那么直接组装一下 url 信息
  if (/^get$/i.test(method) && data) url += '?' + data

  // 4. 发送请求
  const xhr = new XMLHttpRequest()
  xhr.open(method, url, async)
  xhr.onload = function () {
    if (!/^2\d{2}$/.test(xhr.status)) {
      error(`错误状态码:${xhr.status}`)
      return 
    }
    // 执行解析
    try {
      let result = JSON.parse(xhr.responseText)
      success(result)
    } catch (err) {
      error('解析失败 ! 因为后端返回的结果不是 json 格式字符串')
    }
  }

  // 设置请求头内的信息
  for (let k in headers) xhr.setRequestHeader(k, headers[k])
  if (/^get$/i.test(method)) {
    xhr.send()
  } else {
    xhr.send(data)
  }
}

```

```js
ajax({
    url:"http://localhost:3000/users",
    method:"GET",
    async:true,
    data:{
        username:"kerwin",
        password:"123"
    }, 
    headers:{},
    success:function(res){
        console.log(res)
    },
    error:function(err){
        console.log(err)
    }
})
```

##### Promise

- `promise` 是一个 ES6 的语法
- 承诺的意思，是一个专门用来解决异步 **回调地狱** 的问题



###### 回调地狱

- 当一个回调函数嵌套一个回调函数的时候

- 就会出现一个嵌套结构

- 当嵌套的多了就会出现回调地狱的情况

- 比如我们发送三个 ajax 请求

  - 第一个正常发送
  - 第二个请求需要第一个请求的结果中的某一个值作为参数
  - 第三个请求需要第二个请求的结果中的某一个值作为参数

  ```javascript
  ajax({
    url: '我是第一个请求',
    success (res) {
      // 现在发送第二个请求
      ajax({
        url: '我是第二个请求'，
        data: { a: res.a, b: res.b },
        success (res2) {
          // 进行第三个请求
          ajax({
            url: '我是第三个请求',
            data: { a: res2.a, b: res2.b },
    				success (res3) { 
              console.log(res3) 
            }
          })
        }
      })
    }
  })
  ```

- **回调地狱，其实就是回调函数嵌套过多导致的**

![](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/%E5%9B%9E%E8%B0%83%E5%9C%B0%E7%8B%B1.jpeg)

- 当代码成为这个结构以后，已经没有维护的可能了
- 所以我们要把代码写的更加的艺术一些



###### PROMISE

- 为了解决回调地狱

- 我们就要使用 promise 语法

- 必须时promise对象才能调用then方法或catch

- 语法：

  ```javascript
      <script>
          //Promise 构造函数
  
          var q = new Promise(function(resolve,reject){
              //异步
              setTimeout(()=>{
                  //成功兑现承诺
                  // resolve(["1111","222","3333"])
  
                  //失败拒绝承诺
                  reject("errrror")
              },2000)
          })
          //pending 执行中
          //fulfilled
          //reject
  
          //q是promise对象
  
          q.then(function(res){
              //兑现承诺，这个函数被执行
              console.log("success",res)
          }).catch(function(err){
              //拒绝承诺，这个函数就会被执行
              console.log("fail",err)
          })
      </script>
  ```

- promise 就是一个语法

  - 我们的每一个异步事件，在执行的时候
  - 都会有三个状态，执行中 / 成功 / 失败

- 因为它包含了成功的回调函数

- 所以我们就可以使用 promise 来解决多个 ajax 发送的问题

  ```javascript
  new Promise(function (resolve, reject) {
    ajax({
      url: '第一个请求',
      success (res) {
        resolve(res)
      }
    })
  }).then(function (res) {
    // 准备发送第二个请求
    return new Promise(function (resolve, reject) {
      ajax({ 
        url: '第二个请求',
        data: { a: res.a, b: res.b },
        success (res) {
          resolve(res)
        }
      })
    })
  }).then(function (res) {
    ajax({
      url: '第三个请求',
      data: { a: res.a, b: res.b },
      success (res) {
        console.log(res)
      }
    })
  })
  ```

  




##### ASYNC/AWAIT

- `async/await` 是一个 es7 的语法

- 这个语法是 **回调地狱的终极解决方案**

- 语法：

  ```javascript
  async function fn() {
    const res = await promise对象
  }
  ```

- 这个是一个特殊的函数方式

- 可以 await 一个 promise 对象

- **可以把异步代码写的看起来像同步代码**

- 只要是一个 promiser 对象，那么我们就可以使用 `async/await` 来书写

  ```javascript
  async function fn() {
    const res = new Promise(function (resolve, reject) {
      ajax({
        url: '第一个地址',
        success (res) {
          resolve(res)
        }
      })
    })
    
    // res 就可以得到请求的结果
    const res2 = new Promise(function (resolve, reject) {
      ajax({
        url: '第二个地址',
        data: { a: res.a, b: res.b },
        success (res) {
          resolve(res)
        }
      })
    })
    
    const res3 = new Promise(function (resolve, reject) {
      ajax({
        url: '第三个地址',
        data: { a: res2.a, b: res2.b },
        success (res) {
          resolve(res)
        }
      })
    })
    
    // res3 就是我们要的结果
    console.log(res3)
  }
  ```

  - 这样的异步代码写的就看起来像一个同步代码了

  ```js
  function getApiData() {
      // Promise异步编程的一种解决方案
      // 第一个参数是 Promise 执行成功时的回调，第二个参数是 Promise 执行失败时的回调
      return new Promise((resolve, reject) => {
          // 模拟延迟(获取服务的数据) 
         setTimeout(() => {
              // 执行成功
              resolve({name: 'kandy', age: 99})
          }, 3000)
      })
  }
  
  let user = {}
  
  async function getUser() {
      // 执行 
     await getApiData().then(res => {
          user = res
      })
      // await后的该代码块在此会阻塞,直到 getApiData 执行后 then 完成工作后才能继续往下执行    
      console.log('获取数据完成: ', user)
  }
  
  //getUser()  // 异步执行的方法
  //console.log('开始获取数据:')  // 此处无阻塞(同步代码)
  //结果:
  
  //开始获取数据: 
  //3 秒后：
  
  //获取数据完成:  {name: 'kandy', age: 99}
  ```

  

##### fetch

​	*XMLHttpRequest 是一个设计粗糙的 API，配置和调用方式非常混乱， 而且基于事件的异步模型写起来不友好。* 

​	**兼容性不好 polyfill: https://github.com/camsong/fetch-ie8**

```js
fetch("http://localhost:3000/users")
            .then(res=>res.json())
            .then(res=>{
                console.log(res)
            })


fetch("http://localhost:3000/users",{
            method:"POST",
            headers:{
                "content-type":"application/json"
            },
            body:JSON.stringify({
                username:"kerwin",
                password:"123"
            })
        })
            .then(res=>res.json())
            .then(res=>{
                console.log(res)
            })

fetch("http://localhost:3000/users/5",{
            method:"PUT",
            headers:{
                "content-type":"application/json"
            },
            body:JSON.stringify({
                username:"kerwin",
                password:"456"
            })
        })
            .then(res=>res.json())
            .then(res=>{
                console.log(res)
            })

fetch("http://localhost:3000/users/5",{
            method:"DELETE"
        })
            .then(res=>res.json())
            .then(res=>{
                console.log(res)
            })
```

```js
//错误处理
fetch("http://localhost:3000/users1")
            .then(res=>{
                if(res.ok){
                    return res.json()
                }else{
                    return Promise.reject({
                        status:res.status,
                        statusText:res.statusText
                    })
                }
            })
            .then(res=>{
                console.log(res)
            })
            .catch(err=>{
                console.log(err)
            })
```



##### cookie

**cookie的特点**

1. 只能存储文本
2. 单条存储有大小限制4KB左右
   数量限制（一般浏览器，限制大概在50条左右）
3. 读取有域名限制：不可跨域读取，只能由来自 写入cookie的 同一域名 的网页可进行读取。简单的讲就是，哪个服务器发给你的cookie，只有哪个服务器有权利读取
4. 时效限制：每个cookie都有时效，默认的有效期是，会话级别：就是当浏览器关闭，那么cookie立即销毁，但是我们也可以在存储的时候手动设置cookie的过期时间
5. 路径限制：存cookie时候可以指定路径，只允许子路径读取外层cookie，外层不能读取内层。





`localStorage` 和 `cookie` 都是在客户端存储数据的方式，它们之间有以下几点区别：

1. 存储大小：`cookie` 存储大小一般为 4KB 左右，而 `localStorage` 可以存储更大的数据，一般为 5MB 左右。

2. 数据有效期：`cookie` 可以设置过期时间，存储在客户端，并随着每一次 HTTP 请求发送到服务器端，直到过期或被删除；而 `localStorage` 没有过期时间，并且存储在客户端，不会随着 HTTP 请求发送到服务器端。

3. 存储位置：`cookie` 通常存储在内存中，有的浏览器可能会将其存储在本地文件中，而 `localStorage` 存储在客户端的硬盘中。

4. 权限控制：不同的浏览器对 `cookie` 的存储大小和数量有限制，并且 `cookie` 存储数据可以被客户端修改和篡改，容易受到 XSS 攻击；而 `localStorage` 存储大小和数量的限制较小，并且只能被同一客户端修改，相对来说更安全，但也需要注意避免被 CSRF 攻击。

总之，相对于 `cookie`，`localStorage` 可以存储更多数据、更加安全、数据有效期更长，但是它缺少了一些 `cookie` 的优点，如每次请求都会自动发送到服务器端、支持设置过期时间、不同浏览器对其限制较少等。在实际应用中，需要根据具体的需求和情况选择使用 `cookie` 还是 `localStorage`。





##### jsonp

跨域访问数据

Jsonp(JSON with Padding) 是 json 的一种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据。

为什么我们从不同的域（网站）访问数据需要一个特殊的技术( JSONP )呢？这是因为同源策略。



```js
const script = document.createElement('script')
script.src = './kerwin.txt'
document.body.appendChild(script)
```

##### 闭包



​     函数内部返回一个函数，被外界所引用。

​     这个内部函数就不会被销毁回收。

​     内部函数所用到的外部函数的变量也不会被销毁。

​    

```js
for(var i=0;i<oli.length;i++){
            oli[i].onclick = (function(index){
                
                return function(){
                    console.log(11111,index)
                }
            })(i) //匿名自执行函数 想绑定的函数在return中 return中的函数引用了index 保存了临时变量
        }   
```



#### 七. jQuery



- `jQuery` 是一个前端库，也是一个方法库
- 他里面封装着一些列的方法供我们使用
- 我们常用的一些方法它里面都有，我们可以直接拿来使用就行了
- `jQuery` 之所以好用，很多人愿意使用，是因为他的几个优点太强大了
  1. 优质的选择器和筛选器
  2. 好用的隐式迭代
  3. 强大的链式编程
- 因为这些东西的出现，很多时候我们要做的事情被 “一行代码解决”
- 接下来我们就来认识一下 `jQuery`



##### 1. jQuery 的使用

- [jQuery官网](https://jquery.com/)

- [jQuery方法大全中文网](http://jquery.cuishifeng.cn/)

  - 这个网站可以多看看
  - 里面是 `jQuery` 的方法大全，而且是中文的

- 我们要使用 `jQuery` 首先要下载一个

  - 可以去官网下载

- 然后就是再页面里面引入 `jQuery.js` 就行了

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
  </head>
  <body>
    <script src="./jquery/jquery.js"></script>
  </body>
  </html>
  ```

- 然后就可以开始使用了

- `jQuery` 向全局暴露的接口就是 `jQuery` 或者 `$` 都行



##### 2.选择器和筛选器

- 选择器和筛选器就是用来帮我们获取 DOM 元素的



###### 2-1选择器

- `jQuery` 有着相当强大的选择器

  ```javascript
  // 按照 id 获取页面中的元素
  const ele = jQuery('#box') 
  const ele = $('#box')
  ```

  - 上面两个都可以按照 id 来获取元素

  ```javascript
  // 按照类名来选择
  const eles = jQuery('.a')
  const eles = $('.a')
  ```

  - 上面就是按照类名来选择元素，可以获取到一组元素

  ```javascript
  const lis = jQuery('li')
  const lis = $('li')
  ```

  - 上面就是按照标签名来获取元素，可以获取到一组元素

  ```javascript
  const eles = jQuery('ul > li')
  const eles = $('ul > li')
  ```

  - 上面就是按照选择器来获取元素，可以获取到一组元素



###### 2-2特殊选择器

- 直接找到第一个

  ```javascript
  $('li:first') // 找到所有 li 中的第一个
  ```

- 直接找到最后一个

  ```javascript
  $('li:last') // 找到所有 li 中的最后一个
  ```

- 直接找到第几个

  ```javascript
  $('li:eq(3)') // 找到所有 li 中索引为 3 的那个
  ```

- 找到所有奇数个

  ```javascript
  $('li:odd') // 找到所有 li 中索引为 奇数 的
  ```

- 找到所有偶数

  ```javascript
  $('li:even') // 找到所有 li 中索引为 偶数 的
  ```

  

###### 2-3筛选器

- jQuery 的筛选器就是在选择器选择到一组元素以后

- 对元素进行筛选，也可以对准确的某一个元素进行判断和获取

  1. 找到所有元素中的第一个

     ```javascript
     $('li').first()
     ```

  2. 找到所有元素中的最后一个

     ```javascript
     $('li').last()
     ```

  3. 找到某一个元素的下一个兄弟元素

     ```javascript
     $('li:eq(3)').next()
     ```

  4. 找到某一个元素的上一个兄弟元素

     ```javascript
     $('li:eq(3)').prev()
     ```

  5. 找到某一个元素的后面的所有兄弟元素

     ```javascript
     $('li:eq(3)').nextAll()
     ```

  6. 找到某一个元素的前面的所有兄弟元素

     ```javascript
     $('li:eq(3)').prevAll()
     ```

  7. 找到某一个元素的父元素

     ```javascript
     $('li:eq(3)').parent()
     ```

  8. 找到某一个元素的所有结构父级，一直到 html

     ```javascript
     $('li:eq(3)').parents()
     ```

  9. 找到一组元素中的某一个

     ```javascript
     // 在 li 的所有父级里面找到所有 body 标签
     $('li').parents().find('body')
     
     // 找到 div 标签下所有后代元素中所有类名为 box 的元素
     $('div').find('.box')
     ```



##### 3.属性操作

- 给一个元素添加某个属性

  ```javascript
  // 给 div 元素添加一个 id 属性，值是 box
  $('div').prop('id', 'box')
  // 获取 div 的 id 属性
  console.log($('div').prop('id'))
  ```

  - prop 这个方法只能添加元素自己本身就有的属性
  - 如果是添加的自定义属性，不会显示在标签上，但是可以使用

- 给一个元素添加某个自定义属性

  ```javascript
  // 给 div 添加一个 index 属性，值是 1
  $('div').attr('index', 1)
  // 获取 div 的 index 属性
  console.log($('div').attr('index'))
  ```

- 移除元素的某一个属性

  ```javascript
  // 移除元素自己本身的属性
  $('div').removeProp('id')
  // 移除元素的自定义属性
  $('div').removeAttr('index')
  ```

##### 4.操作元素的类名

```js
// 判断某一个元素有没有某一个 class
$('div').hasClass('box') // true 表示该元素有 box 类名，false 表示该元素没有 box 类名

// 给元素添加一个类名
$('div').addClass('box2') // 给 div 元素添加一个 box2 类名

// 移除元素的类名
$('div').removeClass('box') // 移除 div 的 box 类名

// 切换元素类名
$('div').toggleClass('box3') // 如果元素本身有这个类名就移除，本身没有就添加
```



##### 5. 操作元素的内容

```js
给元素的 innerHTML 赋值
$('div').html('<span>hello world</span>')
// 获取元素的 innerHTML
$('div').html()

// 给元素的 innerText 赋值
$('div').text('hello world')
// 获取元素的 innerText
$('div').text()

// 给元素的 value 赋值
$('input').val('admin')
// 获取元素的 value 值
$('input').val()
```



##### 6. 操作样式

- jQuery 操作元素的样式就是一个方法 `css`

  ```javascript
  // 给元素设置一个 css 样式
  $('div').css('width', '100px')
  
  // 获取元素的某一个样式
  $('div').css('width')
  
  // 给元素设置一组样式
  $('div').css({
      width: '100px',
      height: '200px'
  })
  ```

  

##### 7. 元素尺寸

- 操作元素的宽和高

  ```javascript
  // 获取 div 元素内容位置的高，不包含 padding 和 border
  $('div').height()
  // 设置 div 内容位置的高为 200px
  $('div').height(200)
  
  // 获取 div 元素内容位置的宽，不包含 padding 和 border
  $('div').width()
  // 设置 div 内容位置的宽为 200px
  $('div').width(200)
  ```

- 获取元素的内置宽和高

  ```javascript
  // 获取 div 元素内容位置的高，包含 padding 不包含 border
  $('div').innerHeight()
  
  // 获取 div 元素内容位置的宽，包含 padding 不包含 border
  $('div').innerWidth()
  ```

- 获取元素的外置宽和高

  ```javascript
  // 获取 div 元素内容位置的高，包含 padding 和 border
  $('div').outerHeight()
  // 获取 div 元素内容位置的高，包含 padding 和 border 和 margin
  $('div').outerHeight(true)
  
  // 获取 div 元素内容位置的宽，包含 padding 和 border
  $('div').outerWidth()
  // 获取 div 元素内容位置的高，包含 padding 和 border 和 margin
  $('div').outerWidth(true)
  ```



##### 8. 元素位置

- 元素相对页面的位置

  ```javascript
  // 获取 div 相对页面的位置
  $('div').offset() // 得到的是以一个对象 { left: 值, top: 值 }
  
  // 给 div 设置相对页面的位置
  $('div').offset({ left: 100, top: 100 })
  // 获取定位到一个距离页面左上角 100 100 的位置
  ```

- 元素相对于父元素的偏移量

  ```javascript
  // 获取 div 相对于父元素的偏移量（定位的值）
  $('div').position()
  ```

- 获取页面卷去的高度和宽度

  ```javascript
  window.onscroll = function () {
      // 获取浏览器卷去的高度
      console.log($(window).scrollTop())
  }
  
  window.onscroll = function () {
      // 获取浏览器卷去的宽度
      console.log($(window).scrollLeft())
  }
  ```



##### 9. 元素事件

- 绑定事件的方法

  ```javascript
  // 给 button 按钮绑定一个点击事件
  $('button').on('click', function () {
      console.log('我被点击了')
  })
  
  // 给 button 按钮绑定一个点击事件，并且携带参数
  $('button').on('click', { name: 'Jack' }, function (e) {
      console.log(e) // 所有的内容都再事件对象里面
      console.log(e.data) // { name: 'Jack' }
  })
  
  // 事件委托的方式给 button 绑定点击事件
  $('div').on('click', 'button', function () {
      console.log(this) // button 按钮
  })
  
  // 事件委托的方式给 button 绑定点击事件并携带参数
  $('div').on('click', 'button', { name: 'Jack' }, function (e) {
      console.log(this) // button 按钮
      console.log(e.data)
  })
  ```

- 移除事件

  ```javascript
  // 给 button 按钮绑定一个 点击事件，执行 handler 函数
  $('button').on('click', handler)
  
  // 移除事件使用 off
  $('button').off('click', handler)
  ```

- 只能执行一次的事件

  ```javascript
  // 这个事件绑定再 button 按钮身上
  // 当执行过一次以后就不会再执行了
  $('button').one('click', handler)
  ```

- 直接触发事件

  ```javascript
  // 当代码执行到这里的时候，会自动触发一下 button 的 click 事件
  $('button').trigger('click')
  ```



**可以直接使用的常见事件**

- 可以直接使用的事件就是可以不利用 `on` 来绑定，直接就可以使用的事件方法

- `click`

  ```javascript
  // 直接给 div 绑定一个点击事件
  $('div').click(function () {
      console.log('我被点击了')
  })
  
  // 给 div 绑定一个点击事件并传递参数
  $('div').click({ name: 'Jack' }, function (e) {
      console.log(e.data)
  })
  ```

- `dblclick`

  ```javascript
  // 直接给 div 绑定一个双击事件
  $('div').dblclick(function () {
      console.log('我被点击了')
  })
  
  // 给 div 绑定一个双击事件并传递参数
  $('div').dblclick({ name: 'Jack' }, function (e) {
      console.log(e.data)
  })
  ```

- `scroll`

  ```javascript
  // 直接给 div 绑定一个滚动事件
  $('div').scroll(function () {
      console.log('我被点击了')
  })
  
  // 给 div 绑定一个滚动事件并传递参数
  $('div').scroll({ name: 'Jack' }, function (e) {
      console.log(e.data)
  })
  ```

  

##### 10.动画

- `show`

  ```javascript
  // 给 div 绑定一个显示的动画
  $('div').show() // 如果元素本身是 display none 的状态可以显示出来
  
  // 给 div 绑定一个显示的动画
  // 接受三个参数
  // $('div').show('毫秒', '速度', '回调函数') 
  $('div').show(1000, 'linear', function () {
      console.log('我显示完毕')
  }) 
  ```

- `hide`

  ```javascript
  // 给 div 绑定一个隐藏的动画
  $('div').hide() // 如果元素本身是 display block 的状态可以隐藏起来
  
  // 给 div 绑定一个显示的动画
  // 接受三个参数
  // $('div').show('毫秒', '速度', '回调函数') 
  $('div').hide(1000, 'linear', function () {
      console.log('我隐藏完毕')
  }) 
  ```

- `toggle`

  ```javascript
  // 给 div 绑定一个切换的动画
  $('div').hide() // 元素本身是显示，那么就隐藏，本身是隐藏那么就显示
  
  // 给 div 绑定一个显示的动画
  // 接受三个参数
  // $('div').show('毫秒', '速度', '回调函数') 
  $('div').toggle(1000, 'linear', function () {
      console.log('动画执行完毕')
  }) 
  ```

- `animate`

  ```javascript
  // 定义一个自定义动画
  $('.show').click(function () {
      $('div').animate({
          width: 500,
          height: 300
      }, 1000, 'linear', function () {
          console.log('动画运动完毕')
      })
  })
  ```

- `stop`

  ```javascript
  // 立刻定制动画
  $('div').stop() // 就停止再当前状态
  ```

- `finish`

  ```javascript
  // 立刻结束动画
  $('div').finish() // 停止在动画结束状态
  ```

  

##### 11. 元素操作

- 创建一个元素

  ```javascript
  var div = $('<div></div>')
  ```

- 内部插入元素

  ```javascript
  // 向 div 元素中插入一个 p 元素，放在最后
  $('div').append($('<p></p>'))
  
  // 把 p 元素插入到 div 中去，放在最后
  $('<p>hello</p>').appendTo($('div'))
  
  // 向 div 元素中插入一个 p 元素，放在最前
  $('div').prepend($('<p></p>'))
  
  // 把 p 元素插入到 div 中去，放在最前
  $('<p>hello</p>').prependTo($('div'))
  ```

- 外部插入元素

  ```javascript
  // 在 div 的后面插入一个元素 p
  $('div').after($('<p></p>'))
  
  // 在 div 的前面插入一个元素 p
  $('div').before($('<p></p>'))
  
  // 把 p 元素插入到 div 元素的后面
  $('div').insertAfter($('<p></p>'))
  
  // 把 p 元素插入到 div 元素的前面
  $('div').insertBefore($('<p></p>'))
  ```

- 替换元素

  ```javascript
  // 把 div 元素替换成 p 元素
  $('div').replaceWith($('<p></p>'))
  
  // 用 p 元素替换掉 div 元素
  $('<p></p>').replaceAll($('div'))
  ```

- 删除元素

  ```javascript
  // 删除元素下的所有子节点
  $('div').empty()
  
  // 把自己从页面中移除
  $('div').remove()
  ```

- 克隆元素

  ```javascript
  // 克隆一个 li 元素
  // 接受两个参数
  //   参数1： 自己身上的事件要不要复制，默认是 false
  //   参数2： 所有子节点身上的事件要不要复制，默认是 true
  $('li').clone()
  ```





##### 12. 发送 ajax 请求

- 发送 get 请求

  ```javascript
  // 直接使用 $.get 方法来发送一个请求
  /*
  	参数一： 请求地址
  	参数二： 请求时携带的参数
  	参数三： 请求成功的回调
  	参数四： 返回的数据类型
  */
  $.get('./ajax.php', { id: 10 }, function (res) { console.log(res) }, 'json')
  ```

- 发送 post 请求

  ```javascript
  // 直接使用 $.post 方法来发送一个请求
  /*
  	参数一： 请求地址
  	参数二： 请求时携带的参数
  	参数三： 请求成功的回调
  	参数四： 返回的数据类型
  */
  $.post('./ajax.php', { id: 10 }, function (res) { console.log(res) }, 'json')
  ```

- 综合发送 ajax 请求

  ```javascript
  // 使用 $.ajax 方法
  // 只接受一个参数，是一个对象，这个对象对当前的请求进行所有的配置
  $.ajax({
      url: './ajax',   // 必填，请求的地址
      type: 'GET',   // 选填，请求方式，默认是 GET（忽略大小写）
      data: {},   // 选填，发送请求是携带的参数
      dataType: 'json',   // 选填，期望返回值的数据类型
      async: true,   // 选填，是否异步，默认是 true
      success () {},   // 选填，成功的回调函数
      error () {},   // 选填，失败的回调函数
      cache: true,   // 选填，是否缓存，默认是 true
      context: div,   // 选填，回调函数中的 this 指向，默认是 ajax 对象
      status: {},   // 选填，根据对应的状态码进行函数执行
      timeout: 1000,   // 选填，超时事件
  })
  ```

- 发送一个 jsonp 请求

  ```javascript
  // 使用 $.ajax 方法也可以发送 jsonp 请求
  // 只不过 dataType 要写成 jsonp
  $.ajax({
      url: './jsonp.php',
      dataType: 'jsonp',
      data: { name: 'Jack', age: 18 },
      success (res) {
          console.log(res)
      },
      jsonp: 'cb',  // jsonp 请求的时候回调函数的 key
      jsonpCallback: 'fn'   // jsonp 请求的时候回调函数的名称
  })
  ```

  

##### 13. 全局 ajax 函数

- 全局的 `ajax` 函数我们也叫做 **`ajax` 的钩子函数**
- 也就是在一个 `ajax` 的整个过程中的某一个阶段执行的函数
- 而且每一个 `ajax` 请求都会触发



###### ajaxStart

- 任意一个请求在 **开始** 的时候就会触发这个函数

  ```javascript
  $(window).ajaxStart(function () {
      console.log('有一个请求开始了')
  })
  ```





###### ajaxSend

- 任意一个请求在 **准备 send 之前** 会触发这个函数

  ```javascript
  $(window).ajaxSend(function () {
      console.log('有一个要发送出去了')
  })
  ```





###### ajaxSuccess

- 任意一个请求在 **成功** 的时候就会触发这个函数

  ```javascript
  $(window).ajaxSuccess(function () {
      console.log('有一个请求成功了')
  })
  ```





###### ajaxError

- 任意一个请求在 **失败** 的时候就会触发这个函数

  ```javascript
  $(window).ajaxError(function () {
      console.log('有一个请求失败了')
  })
  ```





###### ajaxComplete

- 任意一个请求在 **完成** 的时候就会触发这个函数

  ```javascript
  $(window).ajaxComplete(function () {
      console.log('有一个请求完成了')
  })
  ```





###### ajaxStop

- 任意一个请求在 **结束** 的时候就会触发这个函数

  ```javascript
  $(window).ajaxStop(function () {
      console.log('有一个请求结束了')
  })
  ```



##### 14.jQuery 的多库共存

- 我们一直在使用 `jQuery`，都没有什么问题

- 但是如果有一天，我们需要引入一个别的插件或者库的时候

- 人家也向外暴露的是 `$` 获取 `jQuery`

- 那么，我们的 `jQuery` 就不能用了

- 那么这个时候，`jQuery` 为我们提供了一个多库并存的方法

  ```javascript
  // 这个方法可以交还 jQuery 命名的控制权
  jQuery.noConflict()
  
  // 上面代码执行完毕以后 $ 这个变量就不能用了
  // 但是 jQuery 可以使用
  console.log($) // undefined
  console.log(jQuery) // 可以使用
  ```

- 完全交出控制权

  ```javascript
  // 这个方法可以交并且传递一个 true 的时候，会完全交出控制权
  jQuery.noConflict(true)
  
  // 上面代码执行完毕以后 $ 这个变量就不能用了
  // jQuery 这个变量也不能用了
  console.log($) // undefined
  console.log(jQuery) // undefined
  ```

- 更换控制权

  ```javascript
  // 可以用一个变量来接受返回值，这个变量就是新的控制权
  var aa = jQuery.noConflict(true)
  
  // 接下来就可以把 aa 当作 jQuery 向外暴露的接口使用了
  aa('div').click(function () { console.log('我被点击了') })
  ```

  

##### 15 . JQuery 的插件扩展

- `jQuery` 确实很好很强大
- 但是也有一些方法是他没有的，我们的业务需求中有的时候会遇到一些它里面没有的方法
- 那么我们就可以给他扩展一些方法



###### 扩展给他自己本身

- 扩展给自己本身使用 `jQuery.extend` 这个方法

- 扩展完后的内容只能用 `$` 或者 `jQuery` 来调用

  ```javascript
  // jQuery.extend 接受一个参数，是一个对象，对象里面是我们扩展的方法
  jQuery.extend({
      max: function (...n) { return Math.max.apply(null, n) },
      min: function (...n) { return Math.min.apply(null, n) }
  })
  ```

- 扩展完毕我们就可以使用了

  ```javascript
  const max = $.max(4, 5, 3, 2, 6, 1)
  console.log(max) // 6
  const min = $.min(4, 5, 3, 2, 6, 1)
  console.log(min) // 1
  ```



###### 扩展给元素集

- 扩展完毕以后给元素的集合使用

- 也就是我们用 `$('li')` 这样的选择器获取到的元素集合来使用

- 使用 `jQuery.fn.extend()` 方法来扩展

  ```javascript
  // jQuery.fn.extend() 接受一个参数，是一个对象，对象里面是我们扩展的方法
  jQuery.fn.extend({
      checked: function () {
          // return 关键字是为了保证链式编程
          // 后面的代码才是业务逻辑
          return this.each(function() { this.checked = true })
      }
  })
  ```

- 扩展完毕我们就可以使用了

  ```javascript
  // 靠元素集合来调用
  $('input[type=checkbox]').checked()
  // 执行完毕之后，所有的 复选框 就都是选中状态了
  ```

  