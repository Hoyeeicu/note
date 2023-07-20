#### 二 BOM

- `BOM（Browser Object Model）`： 浏览器对象模型
- 其实就是操作浏览器的一些能力
- 我们可以操作哪些内容
  - 获取一些浏览器的相关信息（窗口的大小）
  - 操作浏览器进行页面跳转
  - 获取当前浏览器地址栏的信息
  - 操作浏览器的滚动条
  - 浏览器的信息（浏览器的版本）
  - 让浏览器出现一个弹出框（`alert` / `confirm` / `prompt`）
  - ...
- `BOM` 的核心就是 `window` 对象
- `window` 是浏览器内置的一个对象，里面包含着操作浏览器的方法



##### 1. 获取浏览器窗口的尺寸

- ` innerHeight` 和 `innerWidth`

- 这两个方法分别是用来获取浏览器窗口的宽度和高度（包含滚动条的）

  ```javascript
  var windowHeight = window.innerHeight
  console.log(windowHeight)
  
  var windowWidth = window.innerWidth
  console.log(windowWidth)
  ```



##### 2. 浏览器的弹出层

- `alert` 是在浏览器弹出一个提示框

  ```javascript
  window.alert('我是一个提示框')
  ```

  ![](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/alert.png)

  - 这个弹出层知识一个提示内容，只有一个确定按钮
  - 点击确定按钮以后，这个提示框就消失了

- `confirm` 是在浏览器弹出一个询问框

  ```javascript
  var boo = window.confirm('我是一个询问框')
  console.log(boo)
  ```

  ![](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/confirm.png)

  - 这个弹出层有一个询问信息和两个按钮
  - 当你点击确定的时候，就会得到 `true`
  - 当你点击取消的时候，就会得到 `false`

- `prompt` 是在浏览器弹出一个输入框

  ```javascript
  var str = window.prompt('请输入内容')
  console.log(str)
  ```

  ![](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/prompt.png)

  - 这个弹出层有一个输入框和两个按钮
  - 当你点击取消的时候，得到的是 `null`
  - 当你点击确定的时候得到的就是你输入的内容



##### 3. 浏览器的地址信息

- 在 `window` 中有一个对象叫做 `location`
- 就是专门用来存储浏览器的地址栏内的信息的



###### location.href⭐

- `location.href` 这个属性存储的是浏览器地址栏内 `url` 地址的信息

  ```javascript
  console.log(window.location.href)
  ```

  - 会把中文变成 `url` 编码的格式

- `location.href` 这个属性也可以给他赋值

  ==实现页面的跳转==

  ```javascript
  window.location.href = './index.html'
  // 这个就会跳转页面到后面你给的那个地址
  ```

实现页面跳转

```javascript
    <button id="btn">下一个页面</button>
    <button id="btn2">刷新</button>
    <script>
        console.log(location.href) //地址

        btn.onclick = function(){
            location.href = "http://www.baidu.com"
        }
        //reload
        btn2.onclick = function(){
            location.reload()
        }
    </script>
```



###### location.reload

- `location.reload()` 这个方法会重新加载一遍页面，就相当于刷新是一个道理

  ```javascript
  window.location.reload()
  ```

  - 注意： **不要写在全局，不然浏览器就会一直处在刷新状态**



##### 4. 浏览器的历史记录

- `window` 中有一个对象叫做 `history`
- 是专门用来存储历史记录信息的



###### history.back⭐

- `history.back` 是用来会退历史记录的，就是回到前一个页面，就相当于浏览器上的 ⬅️ 按钮

  ```javascript
  window.history.back()
  ```

  - 前提是你要有上一条记录，不然就是一直在这个页面，也不会回退



###### history.forword

- `history.forword` 是去到下一个历史记录里面，也就是去到下一个页面，就相当于浏览器上的 ➡️ 按钮

  ```javascript
  window.history.forward()
  ```

  - 前提是你要之前有过回退操作，不然的话你现在就是最后一个页面，没有下一个

###### history.go



##### 5. 浏览器的 onload 事件

- 这个不在是对象了，而是一个事件

- 是在页面所有资源加载完毕后执行的

  ```javascript
  window.onload = function () {
    console.log('页面已经加载完毕')
  }
  ```



###### 5-1 在 html 页面中把 js 写在 head 里面

```html
<html>
  <head>
    <meta charset="UTF-8" />
    <script>
    	// 这个代码执行的时候，body 还没有加载
      // 这个时候我们就获取不到 body 中的那个 div

      // 就需要使用 window.onload 事件
      window.onload = function () {
        // 这个函数会在页面加载完毕以后在执行
        // 那么这个时候页面的 DOM 元素都已经加载了，我们就可以获取 div 了
      }
    </script>
  </head>
  <body>
    <div></div>
  </body>
</html>
```



###### 5-2 在 html 页面中把 js 写在 body 最后面

```html
<html>
  <head>
    <meta charset="UTF-8" />
  </head>
  <body>
    <div></div>

    <script>
    	// 这个代码执行的时候，body 已经加载完毕了
      // 在这里就可以获取到 div，写不写 window.onload 就无所谓了

      window.onload = function () {
        // 这个函数会在页面加载完毕以后在执行
        // 那么这个时候页面的 DOM 元素都已经加载了，我们就可以获取 div 了
      }
    </script>
  </body>
</html>
```





##### 6. 浏览器的 onscroll 事件

- 这个 `onscroll` 事件是当浏览器的滚动条滚动的时候触发

- 或者鼠标滚轮滚动的时候出发

  ```javascript
  window.onscroll = function () {
    console.log('浏览器滚动了')
  }
  ```

  - 注意：**前提是页面的高度要超过浏览器的可是窗口才可以**



##### 7. 浏览器滚动的距离

- 浏览器内的内容即然可以滚动，那么我们就可以获取到浏览器滚动的距离
- 思考一个问题？
  - 浏览器真的滚动了吗？
  - 其实我们的浏览器是没有滚动的，是一直在那里
  - 滚动的是什么？是我们的页面
  - 所以说，**其实浏览器没有动，只不过是页面向上走了**
- 所以，这个已经不能单纯的算是浏览器的内容了，而是我们页面的内容
- 所以不是在用 `window` 对象了，而是使用 `document` 对象

##### 8.打开新的标签页✅

```javascript
    <script>
        //location.href = ""  

        // window.open("")
		//打开新的标签页
        btn.onclick = function(){
            window.open("http://www.baidu.com")
        }

        //window.close()
		//关闭自己
        btn2.onclick = function(){
            window.close()
        }
    </script>
```



###### scrollTop

- 获取的是页面向上滚动的距离

- 一共有两个获取方式

  - `document.body.scrollTop`
  - `document.documentElement.scrollTop`

  ```javascript
  window.onscroll = function () {
    console.log(document.body.scrollTop)
    console.log(document.documentElement.scrollTop)
  }
  ```

  - 两个都是获取页面向上滚动的距离
  - 区别：
    - IE 浏览器
      - 没有 `DOCTYPE` 声明的时候，用这两个都行
      - 有 `DOCTYPE` 声明的时候，只能用 `document.documentElement.scrollTop`
    - Chrome 和 FireFox
      - 没有 `DOCTYPE` 声明的时候，用 `document.body.scrollTop`
      - 有 `DOCTYPE` 声明的时候，用 `document.documentElement.scrollTop`
    - Safari
      - 两个都不用，使用一个单独的方法 `window.pageYOffset `

###### scrollTo

滚动到指定位置

```javascript
        btn.onclick = function(){
            // window.scrollTo(0,0)
            //1. 两个数字

            //2. 对象

            window.scrollTo({
                left:0,
                top:0
            })
```



###### scrollLeft

- 获取页面向左滚动的距离

- 也是两个方法

  - `document.body.scrollLeft`

  - `document.documentElementLeft`

    ```javascript
    window.onscroll = function () {
      console.log(document.body.scrollLeft)
      console.log(document.documentElement.scrollLeft)
    }
    ```

  - 两个之间的区别和之前的 `scrollTop` 一样



##### 9. 本地存储



###### 8-1 localStorage

永久存储 

```js
//增
localStorage.setItem("name","kerwin")
//取
localStorage.getItem("name")
//删
localStorage.removeItem("name")
//清空
localStorage.clear()

```



###### 8-2 sessionStorage

临时存储 关闭页面就丢失

```js
//增
sessionStorage.setItem("name","kerwin")
//取
sessionStorage.getItem("name")
//删
sessionStorage.removeItem("name")
//清空
sessionStorage.clear()
```

只能存储字符串



#### 三. DOM

- `DOM（Document Object Model）`： 文档对象模型
- 其实就是操作 `html` 中的标签的一些能力
- 我们可以操作哪些内容
  - 获取一个元素
  - 移除一个元素
  - 创建一个元素
  - 向页面里面添加一个元素
  - 给元素绑定一些事件
  - 获取元素的属性
  - 给元素添加一些 `css` 样式
  - ...
- `DOM` 的核心对象就是 `docuemnt` 对象
- `document` 对象是浏览器内置的一个对象，里面存储着专门用来操作元素的各种方法
- `DOM`： 页面中的标签，我们通过 `js` 获取到以后，就把这个对象叫做 **DOM 对象**



##### 1. 获取一个元素

- 通过 `js` 代码来获取页面中的标签
- 获取到以后我们就可以操作这些标签了

```javascript
      /*   
          html,head,body 非常规

          常规=>id,class,tag,,,,, */
      

        console.log(document.documentElement) // rem
        console.log(document.head) // 获取head
        console.log(document.body) //获取body
```



###### 1-1 getElementById

- `getElementById` 是通过标签的 `id` 名称来获取标签的

- 因为在一个页面中 `id` 是唯一的，所以获取到的就是一个元素

  ```html
  <body>
    <div id="box"></div>
    <script>
    	var box = document.getElementById('box')
    	console.log(box) // <div></div>
    </script>
  </body>
  ```

  - 获取到的就是页面中的那个 **id 为 box 的 div 标签**



###### 1-2 getElementsByClassName

- `getElementsByClassName` 是用过标签的 `class` 名称来获取标签的

- 因为页面中可能有多个元素的 `class` 名称一样，所以获取到的是一组元素

- 哪怕你获取的 `class` 只有一个，那也是获取一组元素，**只不过这一组中只有一个 DOM 元素而已**

  ```html
  <body>
    <div calss="box"></div>
    <script>
    	var box = document.getElementsByClassName('box')
    	console.log(box) // [<div></div>]
      console.log(box[0]) // <div></div>
    </script>
  </body>
  ```

  - 获取到的是一组元素，是一个长得和数组一样的数据结构，但是不是数组，是 **伪数组**
  - 这个一组数据也是按照索引排列的，所以我们想要准确的拿到这个 `div`，需要用索引来获取



###### 1-3 getElementsByTagName

- `getElementsByTagName` 是用过标签的 标签 名称来获取标签的

- 因为页面中可能有多个元素的 标签 名称一样，所以获取到的是一组元素

- 哪怕真的只有一个这个标签名，那么也是获取一组元素，只不过这一组中只有一个 DOM 元素而已

  ```html
  <body>
    <div></div>
    <script>
    	var box = document.getElementsByTagName('div')
    	console.log(box) // [<div></div>]
      console.log(box[0]) // <div></div>
    </script>
  </body>
  ```

  - 和 `getElementsByClassName` 一样，获取到的是一个长得很像数组的元素
  - 必须要用索引才能得到准确的 `DOM` 元素



###### 1-4 querySelector

- `querySelector` 是按照选择器的方式来获取元素

- 也就是说，按照我们写 `css` 的时候的选择器来获取

- 这个方法只能获取到一个元素，并且是页面中第一个满足条件的元素

  ```javascript
  console.log(document.querySelector('div')) // 获取页面中的第一个 div 元素
  console.log(docuemnt.querySelector('.box')) // 获取页面中第一个有 box 类名的元素
  console.log(document.querySelector('#box')) // 获取页面中第一个 id 名为 box 的元素
  ```



###### 1-5 querySelectorAll

- `querySelectorAll` 是按照选择器的方式来获取元素

- 这个方法能获取到所有满足条件的元素，以一个伪数组的形式返回

  ```javascript
  console.log(document.querySelectorAll('div')) // 获取页面中的所有的 div 元素
  console.log(docuemnt.querySelectorAll('.box')) // 获取页面中所有有 box 类名的元素
  ```

  - 获取到的是一组数据，也是需要用索引来获取到准确的每一个 `DOM` 元素

###### 1-6 getElementsByName

###### 

##### 2. 操作属性

- 通过我们各种获取元素的方式获取到页面中的标签以后
- 我们可以直接操作 `DOM` 元素的属性，就能直接把效果展示在页面上

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
<script>
function changeLink(){
    document.getElementById('myAnchor').innerHTML="RUNOOB";
    document.getElementById('myAnchor').href="//www.runoob.com";
    document.getElementById('myAnchor').target="_blank";
}
</script>
</head>
<body>
 
<a id="myAnchor" href="//www.microsoft.com">Microsoft</a>
<input type="button" onclick="changeLink()" value="修改链接">
 
</body>
</html>

```

属性分类

​	1.元素自带(原生)属性

```js
        box.innerHTML = "22222"

        username.type = "password"

       
        rember.checked = false
```

**一般属性都是要加引号的，特殊的如checked不用加**

​	**2.自定义属性**

​	

```js
        //h5 ===> 约定 data-******  .dataset

        console.log(box2.dataset)

        box2.dataset.xiaoming = "hello3"

        delete box2.dataset.xiaoming
        delete box2.dataset.kerwin
        delete box2.dataset.tiechui


        var oitems = document.getElementsByTagName("li")

        for (var i = 0; i < oitems.length; i++) {
            oitems[i].dataset.index = i
        }
```



###### 2-1 innerHTML

- 获取元素内部的 `HTML` 结构  

  ```html
  <body>
    <div>
      <p>
        <span>hello</span>
      </p>
    </div>
  
    <script>
      var div = document.querySelector('div')
      console.log(div.innerHTML)
        /*
  
            <p>
              <span>hello</span>
            </p>
  
  	  */
    </script>
  </body>
  ```

- 设置元素的内容

  ```html
  <body>
    <div></div>
  
    <script>
      var div = document.querySelector('div')
     	div.innerHTML = '<p>hello</p>'
    </script>
  </body>
  ```

  - 设置完以后，页面中的 `div` 元素里面就会嵌套一个 `p` 元素



###### 2-2 innerText

- 获取元素内部的文本（只能获取到文本内容，获取不到 `html` 标签）

  ```html
  <body>
    <div>
      <p>
        <span>hello</span>
      </p>
    </div>
  
    <script>
      var div = document.querySelector('div')
      console.log(div.innerText) // hello
    </script>
  </body>
  ```

- 可以设置元素内部的文本

  ```html
  <body>
    <div></div>
  
    <script>
      var div = document.querySelector('div')
     	div.innerText = '<p>hello</p>'
    </script>
  </body>
  ```

  - 设置完毕以后，会把 `<p>hello</p>` 当作一个文本出现在 `div` 元素里面，而不会把 `p` 解析成标签



###### 2-3 getAttribute

- 获取元素的某个属性（包括自定义属性）

  ```html
  <body>
    <div a="100" class="box"></div>
  
    <script>
      var div = document.querySelector('div')
     	console.log(div.getAttribute('a')) // 100
      console.log(div.getAttribute('class')) // box
    </script>
  </body>
  ```



###### 2-4 setAttribute

- 给元素设置一个属性（包括自定义属性）

  ```html
  <body>
    <div></div>
  
    <script>
      var div = document.querySelector('div')
     	div.setAttribute('a', 100)
      div.setAttribute('class', 'box')
      console.log(div) // <div a="100" class="box"></div>
    </script>
  </body>
  ```

2-4.1 H5中添加自定义属性





###### 2-5 removeAttribute

- 直接移除元素的某个属性

  ```html
  <body>
    <div a="100" class="box"></div>
  
    <script>
      var div = document.querySelector('div')
     	div.removeAttribute('class')
      console.log(div) // <div a="100"></div>
    </script>
  </body>
  ```



###### 

###### 

###### 2-6 style

- 专门用来给元素添加 `css` 样式的

- 添加的都是行内样式

  ```html
  <body>
    <div></div>
  
    <script>
      var div = document.querySelector('div')
     	div.style.width = "100px"
      div.style.height = "100px"
      div.style.backgroundColor = "pink"
      console.log(div)
      // <div style="width: 100px; height: 100px; background-color: pink;"></div>
    </script>
  </body>
  ```

  - 页面中的 `div` 就会变成一个宽高都是 `100`，背景颜色是粉色

###### 2-7 获取元素的非行间样式

- 我们在操作 `DOM` 的时候，很重要的一点就是要操作元素的 `css` 样式

- 那么在操作 `css` 样式的时候，我们避免不了就要获取元素的样式

- 之前我们说过可以用 `元素.style.xxx` 来获取

- 但是这个方法只能获取到元素 **行间样式**，也就是写在**行内的**样式👍

  ```html
  <style>
    div {
      width: 100px;
    }
  </style>
  <body>
    <div style="height: 100px;">
      <p>我是一个 p 标签</p>
    </div>
  
    <script>
      var oDiv = document.querySelector('div')
  		console.log(oDiv.style.height) // 100px
      console.log(oDIv.style.width) // ''
    </script>
  </body>
  ```

- 不管是外链式还是内嵌式，我们都获取不到该元素的样式

- 这里我们就要使用方法来获取了 **`getComputedStyle`** 和 **`currentStyle`**

- 这两个方法的作用是一样的，只不过一个在 **非 IE** 浏览器，一个在 **IE** 浏览器



**getComputedStyle（非IE使用）**

可读不可写

- **语法：`window.getComputedStyle(元素, null).要获取的属性`**

  ```html
  <style>
    div {
      width: 100px;
    }
  </style>
  <body>
    <div style="height: 100px;">
      <p>我是一个 p 标签</p>
    </div>
  
    <script>
      var oDiv = document.querySelector('div')
  		console.log(window.getComputedStyle(oDiv).width) // 100px
      console.log(window.getComputedStyle(oDiv).height) // 100px
    </script>
  </body>
  ```

  - 这个方法获取行间样式和非行间样式都可以



**currentStyle（IE使用）**



- 语法： `元素.currentStyle.要获取的属性`

  ```html
  <style>
    div {
      width: 100px;
    }
  </style>
  <body>
    <div style="height: 100px;">
      <p>我是一个 p 标签</p>
    </div>
  
    <script>
      var oDiv = document.querySelector('div')
  		console.log(oDiv.currentStyle.width) // 100px
      console.log(oDiv.currentStyle.height) // 100px
    </script>
  </body>
  ```

  

###### 2-8 className

- 专门用来操作元素的 **类名的**

  ```html
  <body>
    <div class="box"></div>
  
    <script>
      var div = document.querySelector('div')
     	console.log(div.className) // box
    </script>
  </body>
  ```

- 也可以设置元素的类名，不过是全覆盖式的操作

  ```html
  <body>
    <div class="box"></div>
  
    <script>
      var div = document.querySelector('div')
     	div.className = 'test'
      console.log(div) // <div class="test"></div>
    </script>
  </body>
  ```

  - 在设置的时候，不管之前有没有类名，都会全部被设置的值覆盖

###### **2-9classList添加删除class**✅

  也是操作类名的，但是相对于classname更加细致，没那么暴力

```js
       // classList属性

        console.log(box.classList)

        box.classList.add("item2")

        box.classList.remove("item2")
        box.classList.remove("item1")


        //切换 toggle

        //toggle-有就删除无就添加
        btn.onclick = function(){
            box.classList.toggle("item")
        }
```





##### 3. DOM节点

- `DOM` 的节点我们一般分为常用的三大类 **元素节点** / **文本节点** / **属性节点**
- 什么是分类，比如我们在获取元素的时候，通过各种方法获取到的我们叫做元素节点（标签节点）
- 比如我们标签里面写的文字，那么就是文本节点
- 写在每一个标签上的属性，就是属性节点



###### 3-1 元素节点

- 我们通过 `getElementBy...` 获取到的都是元素节点



###### 3-2 属性节点

- 我们通过 `getAttribute` 获取的就是元素的属性节点



###### 3-3 文本节点

- 我们通过 `innerText` 获取到的就是元素的文本节点


![image-20220529093256532](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220529093256532.png)

![image-20220529093305827](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220529093305827.png)

![image-20220529093325381](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220529093325381.png)

![image-20220529093334602](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220529093334602.png)

![image-20220529093346903](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220529093346903.png)

![image-20220529093416413](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220529093416413.png)

###### 3-4 获取节点

- `childNodes`：获取某一个节点下 **所有的子一级节点**

  ```html
  <body>
    <div>
      <p>hello</p>
    </div>
    
    <script>
      // 这个 oDiv 获取的是页面中的 div 元素，就是一个元素节点
    	var oDiv = document.querySelector('div')
      
      console.log(oDiv.childNodes) 
      /*
      	NodeList(3) [text, p, text]
        0: text
        1: p
        2: text
        length: 3
        __proto__: NodeList
      */
    </script>
  </body>
  ```

  - 我们会发现，拿到以后是一个伪数组，里面有三个节点
  - 一个 `text`：从 `<div> 一直到 <p>` 中间有一个换行和一堆空格，这个是第一个节点，是一个文本节点
  - 一个 `p`：这个 `p` 标签就是第二个节点，这个是一个元素节点
  - 一个 `text`：从 `</p> 一直到 </div>` 中间有一个换行和一堆空格，这个是第三个节点，是一个文本节点
  - 这个时候就能看到我们有不同的节点类型了

- `children` ：获取某一节点下所有的子一级 **元素节点**

  ```html
  <body>
    <div>
      <p>hello</p>
    </div>
    
    <script>
      // 这个 oDiv 获取的是页面中的 div 元素，就是一个元素节点
    	var oDiv = document.querySelector('div')
      
      console.log(oDiv.children) 
      /*
      	HTMLCollection [p]
        0: p
        length: 1
        __proto__: HTMLCollection
      */
    </script>
  </body>
  ```

  - 我们发现只有一个节点了，因为 `children` 只要元素节点
  - div 下面又只有一个元素节点，就是 `p`
  - 所以就只有一个，虽然只有一个，但是也是一个 **伪数组**

- `firstChild`：获取某一节点下子一级的 **第一个节点**

  ```html
  <body>
    <div>
      <p>hello</p>
    </div>
    
    <script>
      // 这个 oDiv 获取的是页面中的 div 元素，就是一个元素节点
    	var oDiv = document.querySelector('div')
      
      console.log(oDiv.firstChild) // #text 
    </script>
  </body>
  ```

  - 这个是只获取一个节点，不再是伪数组了
  - 获取的是第一个
  - 第一个就是 `<div> 一直到 <p>` 的那个换行和空格，是个文本节点

- `lastChild`：获取某一节点下子一级的 **最后一个节点**

  ```html
  <body>
    <div>
      <p>hello</p>
    </div>
    
    <script>
      // 这个 oDiv 获取的是页面中的 div 元素，就是一个元素节点
    	var oDiv = document.querySelector('div')
      
      console.log(oDiv.lastChild) // #text 
    </script>
  </body>
  ```

  - 只获取一个节点，不再是伪数组
  - 获取的是最后一个
  - 最后一个就是 `</p> 一直到 </div>` 之间的换行和空格，是个文本节点

- `firstElementChild`：获取某一节点下子一级 **第一个元素节点**

  ```html
  <body>
    <div>
      <p>hello</p>
    </div>
    
    <script>
      // 这个 oDiv 获取的是页面中的 div 元素，就是一个元素节点
    	var oDiv = document.querySelector('div')
      
      console.log(oDiv.firstElementChild) // <p>hello</p>
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是第一个 **元素节点**
  - 第一个元素节点就是 `p` 标签，是一个元素节点

- `lastElementChild`：获取某一节点下子一级 **最后一个元素节点**

  ```html
  <body>
    <div>
      <p>hello</p>
      <p>world</p>
    </div>
    
    <script>
      // 这个 oDiv 获取的是页面中的 div 元素，就是一个元素节点
    	var oDiv = document.querySelector('div')
      
      console.log(oDiv.lastElementChild) // <p>world</p>
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是最后一个 **元素节点**
  - 最后一个元素节点是 `<p>world</p>`，是一个元素节点

- `nextSibling`：获取某一个节点的 **下一个兄弟节点**

  ```html
  <body>
    <ul>
      <li id="a">hello</li>
      <li id="b">world</li>
      <li id="c">!!!</li>
    </ul>
    
    <script>
      // 这个 oLi 获取的是页面中的 li 元素，就是一个元素节点
    	var oLi = document.querySelector('#b')
      
      console.log(oLi.nextSibling) // #text
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是 `id="b"` 这个 `li` 的下一个兄弟节点
  - 因为 `id="b"` 的下一个节点，是两个 `li` 标签之间的换行和空格，所以是一个文本节点

- `previousSibling`：获取某一个节点的 **上一个兄弟节点**

  ```html
  <body>
    <ul>
      <li id="a">hello</li>
      <li id="b">world</li>
      <li id="c">!!!</li>
    </ul>
    
    <script>
      // 这个 oLi 获取的是页面中的 li 元素，就是一个元素节点
    	var oLi = document.querySelector('#b')
      
      console.log(oLi.previousSibling) // #text
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是 `id="b"` 这个 `li` 的上一个兄弟节点
  - 因为 `id="b"` 的上一个节点，是两个 `li` 标签之间的换行和空格，所以是一个文本节点

- `nextElementSibling`：获取某一个节点的 **下一个元素节点**

  ```html
  <body>
    <ul>
      <li id="a">hello</li>
      <li id="b">world</li>
      <li id="c">!!!</li>
    </ul>
    
    <script>
      // 这个 oLi 获取的是页面中的 li 元素，就是一个元素节点
    	var oLi = document.querySelector('#b')
      
      console.log(oLi.nextElementSibling) // <li id="c">!!!</li>
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是 `id="b"` 这个 `li` 的下一个兄弟元素节点
  - 因为 `id="b"` 的下一个兄弟元素节点就是 `id="c"` 的 `li`，是一个元素节点

- `previousElementSibling`：获取某一个节点的 **上一个元素节点**

  ```html
  <body>
    <ul>
      <li id="a">hello</li>
      <li id="b">world</li>
      <li id="c">!!!</li>
    </ul>
    
    <script>
      // 这个 oLi 获取的是页面中的 li 元素，就是一个元素节点
    	var oLi = document.querySelector('#b')
      
      console.log(oLi.previousElementSibling) // <li id="a">hello</li>
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是 `id="b"` 这个 `li` 的上一个兄弟元素节点
  - 因为 `id="b"` 的上一个兄弟元素节点就是 `id="a"` 的 `li`，是一个元素节点

- `parentNode`：获取某一个节点的 **父节点**

  ```html
  <body>
    <ul>
      <li id="a">hello</li>
      <li id="b">world</li>
      <li id="c">!!!</li>
    </ul>
    
    <script>
      // 这个 oLi 获取的是页面中的 li 元素，就是一个元素节点
    	var oLi = document.querySelector('#b')
      
      console.log(oLi.parentNode) // <ul>...</ul>
    </script>
  </body>
  ```

  - 只获取一个节点，不在是伪数组
  - 获取的是当前这个 `li` 的父元素节点
  - 因为这个 `li` 的父亲就是 `ul`，所以获取到的就是 `ul`，是一个元素节点

- `attributes`：获取某一个 **元素节点** 的所有 **属性节点**

  ```html
  <body>
    <ul>
      <li id="a" a="100" test="test">hello</li>
    </ul>
    
    <script>
      // 这个 oLi 获取的是页面中的 li 元素，就是一个元素节点
    	var oLi = document.querySelector('#a')
      
      console.log(oLi.attributes) 
      /*
      	NamedNodeMap {0: id, 1: a, 2: test, id: id, a: a, test: test, length: 3}
        0: id
        1: a
        2: test
        length: 3
        a: a
        id: id
        test: test
        __proto__: NamedNodeMap
      
      */
    </script>
  </body>
  ```

  - 获取的是一组数据，是该元素的所有属性，也是一个伪数组
  - 这个 `li` 有三个属性，`id` / `a` / `test` 三个，所以就获取到了这三个

##### 4. 节点属性

- 我们已经知道节点会分成很多种，而且我们也能获取到各种不同的节点

- 接下来我们就来聊一些各种节点之间属性的区别

- 我们先准备一段代码

  ```html
  <body>
    <ul test="我是 ul 的一个属性">
      <li>hello</li>
    </ul>
  
    <script>
      // 先获取 ul
      var oUl = document.querySelector('ul')
      
      // 获取到 ul 下的第一个子元素节点，是一个元素节点
      var eleNode = oUl.firstElementChild
      
      // 获取到 ul 的属性节点组合，因为是个组合，我们要拿到节点的话要用索引
      var attrNode = oUl.attributes[0]
  
      // 获取到 ul 下的第一个子节点，是一个文本节点
      var textNode = oUl.firstChild
    </script>
  </body>
  ```

  



###### nodeType

- `nodeType`：获取节点的节点类型，用数字表示

  ```javascript
  console.log(eleNode.nodeType) // 1
  console.log(attrNode.nodeType) // 2
  console.log(textNode.nodeType) // 3
  ```

  - `nodeType === 1` 就表示该节点是一个 **元素节点**
  - `nodeType === 2` 就表示该节点是一个 **属性节点**
  - `nodeType === 3` 就表示该节点是一个 **注释节点**



###### nodeName

- `nodeName`：获取节点的节点名称

  ```javascript
  console.log(eleNode.nodeName) // LI
  console.log(attrNode.nodeName) // test
  console.log(textNode.nodeName) // #text
  ```

  - 元素节点的 `nodeName` 就是 **大写标签名**
  - 属性节点的 `nodeName` 就是 **属性名**
  - 文本节点的 `nodeName` 都是 **#text**



###### nodeValue

- `nodeValue`： 获取节点的值

  ```javascript
  console.log(eleNode.nodeValue) // null
  console.log(attrNode.nodeValue) // 我是 ul 的一个属性
  console.log(textNode.nodeValue) // 换行 + 空格
  ```

  - 元素节点没有 `nodeValue`
  - 属性节点的 `nodeValue` 就是 **属性值**
  - 文本节点的 `nodeValue` 就是 **文本内容**



###### 汇总

| -        | nodeType | nodeName   | nodeValue |
| -------- | -------- | ---------- | --------- |
| 元素节点 | 1        | 大写标签名 | null      |
| 属性节点 | 2        | 属性名     | 属性值    |
| 文本节点 | 3        | \#text     | 文本内容  |



##### 5. 操作 DOM 节点

- 我们所说的操作无非就是 **增删改查（CRUD）**
- 创建一个节点（因为向页面中增加之前，我们需要先创建一个节点出来）
- 向页面中增加一个节点
- 删除页面中的某一个节点
- 修改页面中的某一个节点
- 获取页面中的某一个节点



###### 创建一个节点

- `createElement`：用于创建一个元素节点

  ```javascript
  // 创建一个 div 元素节点
  var oDiv = document.createElement('div')
  
  console.log(oDiv) // <div></div>
  ```

  - 创建出来的就是一个可以使用的 div 元素

- `createTextNode`：用于创建一个文本节点

  ```javascript
  // 创建一个文本节点
  var oText = document.createTextNode('我是一个文本')
  
  console.log(oText) // "我是一个文本"
  ```



###### 向页面中加入一个节点

- `appendChild`：是向一个元素节点的末尾追加一个节点

- 语法： `父节点.appendChild(要插入的子节点)`

  ```javascript
  // 创建一个 div 元素节点
  var oDiv = document.createElement('div')
  var oText = document.createTextNode('我是一个文本')
  
  // 向 div 中追加一个文本节点
  oDiv.appendChild(oText)
  
  console.log(oDiv) // <div>我是一个文本</div>
  ```

- `insertBefore`：向某一个节点前插入一个节点

- 语法： `父节点.insertBefore(要插入的节点，插入在哪一个节点的前面)`

  ```html
  <body>
    <div>
      <p>我是一个 p 标签</p>
    </div>
    
    <script>
    	var oDiv = document.querySelector('div')
      var oP = oDiv.querySelector('p')
      
      // 创建一个元素节点
      var oSpan = document.createElement('span')
      
      // 将这个元素节点添加到 div 下的 p 的前面
      oDiv.insertBefore(oSpan, oP)
      
      console.log(oDiv)
      /*
      	<div>
      		<span></span>
      		<p>我是一个 p 标签</p>
      	</div>
      */
    </script>
  </body>
  ```



###### 删除页面中的某一个节点

- `removeChild`：移除某一节点下的某一个节点

- 语法：`父节点.removeChild(要移除的字节点)`

  ```html
  <body>
    <div>
      <p>我是一个 p 标签</p>
    </div>
    
    <script>
    	var oDiv = document.querySelector('div')
      var oP = oDiv.querySelector('p')
      
      // 移除 div 下面的 p 标签
      oDiv.removeChild(oP)
      
      console.log(oDiv) // <div></div>
    </script>
  </body>
  ```

```js
//this.parentNode.remove()
//删除父节点  严格区分大小写
```



###### 修改页面中的某一个节点

- `replaceChild`：将页面中的某一个节点替换掉

- 语法： `父节点.replaceChild(新节点，旧节点)`

  ```html
  <body>
    <div>
      <p>我是一个 p 标签</p>
    </div>
    
    <script>
    	var oDiv = document.querySelector('div')
      var oP = oDiv.querySelector('p')
      
      // 创建一个 span 节点
      var oSpan = document.createElement('span')
      // 向 span 元素中加点文字
      oSpan.innerHTML = '我是新创建的 span 标签'
      
     	// 用创建的 span 标签替换原先 div 下的 p 标签
      oDiv.replaceChild(oSpan, oP)
      
      console.log(oDiv)
      /*
      	<div>
      		<span>我是新创建的 span 标签</span>
      	</div>
      */
    </script>
  </body>
  ```

##### 6. 获取元素的偏移量

- 就是元素在页面上相对于参考父级的左边和上边的距离



###### offsetParent

- 获取元素的偏移量参考父级
- 其实就是假设你要给一个元素 **绝对定位** 的时候
- 它是根据谁来进行定位的
- 那么这个元素的偏移量参考父级就是谁



###### offsetLeft 和 offsetTop

- 获取的是元左边的偏移量和上边的偏移量
- `offsetLeft` ： 该元素相对于参考父级的左侧偏移量
- `offsetTop` ： 该元素相对于参考父级的上侧偏移量





##### 7. 获取元素尺寸

- 就是获取元素的 "占地面积"



###### offsetWith 和 offsetHeight

- `offsetWidth` ： 获取的是元素 内容 + padding + border 的宽度
- `offsetHeight` ： 获取的是元素 内容 + padding + border 的高度



###### clientWidth 和 clientHeight

- `clientWidth` ： 获取的是元素 内容 + padding 的宽度

- `clientHeight` ： 获取的是元素 内容 + padding 的高度



注意:

- 获取到的尺寸是没有单位的数字
- 当元素在页面中不占位置的时候， 获取到的是 0
  - `display: none;` 元素在页面不占位
  - `visibility: hidden;` 元素在页面占位





##### 8. 获取浏览器窗口尺寸

- 我们之前学过一个 `innerWidth` 和 `innerHeight`
- 他们获取到的是窗口包含滚动条的尺寸
- 下面我们学习两个不包含滚动条的尺寸获取方式



- `document.documentElement.clientWidth` ： 可视窗口的宽度
- `document.documentElement.clientHeight` ： 可视窗口的高度

##### 9. 事件

- 一个事件由什么东西组成

  - 触发谁的事件：事件源
  - 触发什么事件：事件类型
  - 触发以后做什么：事件处理函数

  ```javascript
  var oDiv = document.querySelector('div')
  
  oDiv.onclick = function () {}
  // 谁来触发事件 => oDiv => 这个事件的事件源就是 oDiv
  // 触发什么事件 => onclick => 这个事件类型就是 click
  // 触发之后做什么 => function () {} => 这个事件的处理函数
  ```

  - 我们想要在点击 div 以后做什么事情，就把我们要做的事情写在事件处理函数里面

  ```javascript
  var oDiv = document.querySelector('div')
  
  oDiv.onclick = function () {
    console.log('你点击了 div')
  }
  ```

  - 当我们点击 `div` 的时候，就会执行事件处理函数内部的代码
  - 每点击一次，就会执行一次事件处理函数

##### 10 事件的绑定方式

- 我们现在给一个注册事件都是使用 `onxxx` 的方式

- 但是这个方式不是很好，只能给一个元素注册一个事件

- 一旦写了第二个事件，那么第一个就被覆盖了

  ```javascript
  oDiv.onclick = function () {
    console.log('我是第一个事件')
  }
  
  oDiv.onclick = function () {
    console.log('我是第二个事件')
  }
  ```

  - 当你点击的时候，只会执行第二个，第一个就没有了

- 我们还有一种事件监听的方式去给元素绑定事件

- 使用 `addEventListener` 的方式添加

  - 这个方法不兼容，在 IE 里面要使用 `attachEvent`

- `addEventListener` :  非 IE 7 8 下使用

- 语法： `元素.addEventListener('事件类型'， 事件处理函数， 冒泡还是捕获)`

  ```javascript
  oDiv.addEventListener('click', function () {
    console.log('我是第一个事件')
  }, false)
  
  oDiv.addEventListener('click', function () {
    console.log('我是第二个事件')
  }, false)
  //true就是允许捕获过程出发，false就是只触发冒泡过程，默认值为false
  ```

  - 当你点击 div 的时候，两个函数都会执行，并且会按照你注册的顺序执行
  - 先打印 `我是第一个事件` 再打印 `我是第二个事件`
  - 注意： **事件类型的时候不要写 on，点击事件就是 click，不是 onclick**

- `attachEvent` ：IE 7 8 下使用

- 语法： `元素.attachEvent('事件类型'， 事件处理函数)`

  ```javascript
  oDiv.attachEvent('onclick', function () {
    console.log('我是第一个事件')
  })
  
  oDiv.attachEvent('onclick', function () {
    console.log('我是第二个事件')
  })
  ```

  - 当你点击 div 的时候，两个函数都会执行，并且会按照你注册的顺序倒叙执行
  - 先打印 `我是第二个事件` 再打印 `我是第一个事件`
  - 注意： **事件类型的时候要写 on，点击事件就行 onclick**

**两个方式的区别**

- 注册事件的时候事件类型参数的书写
  - `addEventListener` ： 不用写 on
  - `attachEvent` ： 要写 on
- 参数个数
  - `addEventListener` ： 一般是三个常用参数
  - `attachEvent` ： 两个参数
- 执行顺序
  - `addEventListener` ： 顺序注册，顺序执行
  - `attachEvent` ： 顺序注册，倒叙执行
- 适用浏览器
  - `addEventListener` ： 非 IE 7 8 的浏览器
  - `attachEvent` ： IE 7 8 浏览器



##### 11. 常见的事件

- 我们在写页面的时候经常用到的一些事件
- 大致分为几类，**浏览器事件** / **鼠标事件** / **键盘事件** / **表单事件** / **触摸事件**
- 不需要都记住，但是大概要知道

###### ==classP98==

###### 浏览器事件

- `load` ： 页面全部资源加载完毕
- `scroll` ： 浏览器滚动的时候触发
- ...



###### 鼠标事件

- `click` ：点击事件
- `dblclick` ：双击事件
- `contextmenu` ： 右键单击事件
- `mousedown` ：鼠标左键按下事件
- `mouseup` ：鼠标左键抬起事件
- `mousemove` ：鼠标移动
- `mouseover` ：鼠标移入事件
- `mouseout` ：鼠标移出事件
- `mouseenter` ：鼠标移入事件
- `mouseleave` ：鼠标移出事件
- ...



###### 键盘事件

- `keyup` ： 键盘抬起事件

- `keydown` ： 键盘按下事件

- `keypress` ： 键盘按下再抬起事件

  ```html
      <script>
          // window,document, 输入框 input
  
          username.onkeydown = function(){
              console.log("按下键盘","判读是不是回车键")
          }
  
          username.onkeyup = function(){
              console.log("抬起键盘","判读是不是回车键")
          }
      </script>
  ```

  



###### 表单事件

- `change` : 表单内容改变事件
- `input` : 表单内容输入事件
- `submit` : 表单提交事件
- onfocus
- onblur
- onchange
- oninput
- onsubmit
- onreset

###### 触摸事件

- `touchstart` ： 触摸开始事件
- `touchend` ： 触摸结束事件
- `touchmove` ： 触摸移动事件
- ...

##### 12. 事件对象

- 什么是事件对象？

- 就是当你触发了一个事件以后，对该事件的一些描述信息

- 例如：

  - 你触发一个点击事件的时候，你点在哪个位置了，坐标是多少
  - 你触发一个键盘事件的时候，你按的是哪个按钮
  - ...

- 每一个事件都会有一个对应的对象来描述这些信息，我们就把这个对象叫做 **事件对象**

- 浏览器给了我们一个 **黑盒子**，叫做 `window.event`，就是对事件信息的所有描述

  - 比如点击事件
  - 你点在了 `0，0` 位置，那么你得到的这个事件对象里面对应的就会有这个点位的属性
  - 你点在了 `10, 10` 位置，那么你得到的这个事件对象里面对应的就会有这个点位的属性
  - ...

  ```javascript
  oDiv.onclick = function () {
    console.log(window.event.X轴坐标点信息)
    console.log(window.event.Y轴坐标点信息)
  }
  ```

- 这个玩意很好用，但是一般来说，好用的东西就会有 **兼容性问题**

- 在 `IE低版本` 里面这个东西好用，但是在 `高版本IE` 和 `Chrome` 里面不好使了

- 我们就得用另一种方式来获取 **事件对象**

- 在每一个事件处理函数的行参位置，默认第一个就是 **事件对象**

  ```javascript
  oDiv.onclick = function (e) {
    // e 就是和 IE 的 window.event 一样的东西
    console.log(e.X轴坐标点信息)
    console.log(e.Y轴坐标点信息)
  }
  ```

- 综上所述，我们以后在每一个事件里面，想获取事件对象的时候，都用兼容写法

  ```javascript
  oDiv.onclick = function (e) {
    e = e || window.event
    console.log(e.X轴坐标点信息)
    console.log(e.Y轴坐标点信息)
  }
  ```



```html
 <script>
        box.onclick = function(evt){
            console.log(evt.clientX,evt.clientY)
            console.log(evt.pageX,evt.pageY)

            console.log(evt.offsetX,evt.offsetY)
        }
        //clientX clientY 距离浏览器可视窗口的左上角的坐标值

        //pageX pageY 距离页面文档流的左上角的坐标值


        //offsetX offsetY 距离触发元素的左上角的坐标值
    </script>
```



###### 点击事件的光标坐标点获取

<img src="https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220530215226855.png" alt="image-20220530215226855" style="zoom: 67%;" />

<img src="https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220530220140448.png" alt="image-20220530220140448" style="zoom: 67%;" />

<img src="https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220530220229523.png" alt="image-20220530220229523" style="zoom: 67%;" />







##### 13. 事件的传播dom事件流

![image-20220601095555972](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20220601095555972.png)

  - **当元素触发一个事件的时候，其父元素也会触发相同的事件，父元素的父元素也会触发相同的事件**
  - 就像上面的图片一样
  - 点击在红色盒子上的时候，会触发红色盒子的点击事件
  - 也是点击在了粉色的盒子上，也会触发粉色盒子的点击事件
  - 也是点击在了 body 上，也会触发 body 的点击事件
  - 也是点击在了 html 上，也会触发 html 的点击事件
  - 也是点击在了 document 上，也会触发 document 的点击事件
  - 也是点击在了 window 上，也会触发 window 的点击事件
  - 也就是说，页面上任何一个元素触发事件，都会一层一层最终导致 window 的相同事件触发，前提是各层级元素得有注册相同的事件，不然不会触发
- 在事件传播的过程中，有一些注意的点：
  1. 只会传播同类事件
  2. 只会从点击元素开始按照 html 的结构逐层向上元素的事件会被触发
  3. 内部元素不管有没有该事件，只要上层元素有该事件，那么上层元素的事件就会被触发
- 到现在，我们已经了解了事件的传播，我们再来思考一个问题
  - 事件确实会从自己开始，到 window 的所有相同事件都会触发
  - 是因为我们点在自己身上，也确实逐层的点在了直至 window 的每一个元素身上
  - 但是到底是先点在自己身上，还是先点在了 window 身上呢
  - 先点在自己身上，就是先执行自己的事件处理函数，逐层向上最后执行 window 的事件处理函数
  - 反之，则是先执行 window 的事件处理函数，逐层向下最后执行自己身上的事件处理函数



###### 冒泡、捕获、目标

- 我们刚才聊过了，每一个事件，都是有可能从自己到 window ，有可能要执行多个同类型事件
- 那么这个执行的顺序就有一些说法了



**目标**

- 你是点击在哪个元素身上了，那么这个事件的 **目标** 就是什么



**冒泡**

- 就是从事件 **目标** 的事件处理函数开始，依次向外，直到 window 的事件处理函数触发
- 也就是从下向上的执行事件处理函数



**捕获**

- 就是从 window 的事件处理函数开始，依次向内，只要事件 **目标** 的事件处理函数执行
- 也就是从上向下的执行事件处理函数



###### 如何阻止事件的传播

```js
 function handler(evt){
             //阻止事件传播
            evt.stopPropagation()

            //ie
            // evt.cancelBubble = true
            // console.log(this.parentNode)
            this.parentNode.parentNode.removeChild(this.parentNode)
```

###### **冒泡和捕获的区别**

- 就是在事件的传播中，多个同类型事件处理函数的执行顺序不同

| /*   |                                                             |
| ---- | ----------------------------------------------------------- |
|      | 标准的dom事件流：                                           |
|      | 捕获：window=>docuemtn=>body=>outer                         |
|      | 目标： inner                                                |
|      | 冒泡： outer=>body=>docuemnt=>window、                      |
|      |                                                             |
|      | ie 低版本                                                   |
|      | 只支持冒泡                                                  |
|      |                                                             |
|      |                                                             |
|      | 默认情况 只在冒泡触发                                       |
|      | 按照dom2事件绑定，并进行配置 才能看到捕获的回调函数被触发。 |
|      | */                                                          |

##### 14. 事件委托

- 就是把我要做的事情委托给别人来做
- 因为我们的冒泡机制，点击子元素的时候，也会同步触发父元素的相同事件
- 所以我们就可以把子元素的事件委托给父元素来做



###### 事件触发

- 点击子元素的时候，不管子元素有没有点击事件，只要父元素有点击事件，那么就可以触发父元素的点击事件

  ```html
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
    <script>
    	var oUl = docuemnt.querySelector('ul')
      
      oUl.addEventListener('click', function (e) {
        console.log('我是 ul 的点击事件，我被触发了')
      })
    </script>
  </body>
  ```

  - 像上面一段代码，当你点击 ul 的时候肯定会触发
  - 但是当你点击 li 的时候，其实也会触发



###### target

- target 这个属性是事件对象里面的属性，表示你点击的目标

- 当你触发点击事件的时候，**你点击在哪个元素上，target 就是哪个元素**

- 这个 target 也不兼容，在 IE 下要使用 srcElement

  ```html
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
    <script>
    	var oUl = docuemnt.querySelector('ul')
      
      oUl.addEventListener('click', function (e) {
        e = e || window.event
        var target = e.target || e.srcElement
        console.log(target)
      })
    </script>
  </body>
  ```

  - 上面的代码，当你点击 ul 的时候，target 就是 ul
  - 当你点击在 li 上面的时候，target 就是 li



###### 委托

- 这个时候，当我们点击 li 的时候，也可以触发 ul 的点事件

- 并且在事件内不，我们也可以拿到你点击的到底是 ul 还是 li

- 这个时候，我们就可以把 li 的事件委托给 ul 来做

  ```html
  <body>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
    <script>
    	var oUl = docuemnt.querySelector('ul')
      
      oUl.addEventListener('click', function (e) {
        e = e || window.event
        var target = e.target || e.srcElement
       
        // 判断你点击的是 li
        if (target.nodeName.toUpperCase === 'LI') {
        	// 确定点击的是 li
          // 因为当你点击在 ul 上面的时候，nodeName 应该是 'UL'
          // 去做点击 li 的时候该做的事情了
          console.log('我是 li，我被点击了')
        }
      })
    </script>
  </body>
  ```

  - 上面的代码，我们就可以把 li 要做的事情委托给 ul 来做

##### 15. 默认行为

- 默认行为，就是不用我们注册，它自己就存在的事情
  - 比如我们点击鼠标右键的时候，会自动弹出一个菜单
  - 比如我们点击 a 标签的时候，我们不需要注册点击事件，他自己就会跳转页面
  - ...
- 这些不需要我们注册就能实现的事情，我们叫做 **默认事件**



###### 阻止默认行为

- 有的时候，我们不希望浏览器执行默认事件

  - 比如我给 a 标签绑定了一个点击事件，我点击你的时候希望你能告诉我你的地址是什么
  - 而不是直接跳转链接
  - 那么我们就要把 a 标签原先的默认事件阻止，不让他执行默认事件

- 我们有两个方法来阻止默认事件

  - `e.preventDefault()` : 非 IE 使用
  - `e.returnValue = false` ：IE 使用

- 我们阻止默认事件的时候也要写一个兼容的写法

  ```html
  <a href="https://www.baidu.com">点击我试试</a>
  <script>
  	var oA = document.querySelector('a')
    
    a.addEventListener('click', function (e) {
      e = e || window.event
      
      console.log(this.href)
      
      e.preventDefault ? e.preventDefault() : e.returnValue = false
    })
  </script>
  ```

  - 这样写完以后，你点击 a 标签的时候，就不会跳转链接了
  - 而是会在控制台打印出 a 标签的 href 属性的值

##### 16. this 关键字

- 每一个函数内部都有一个关键字是 `this` 

- 可以让我们直接使用的

- 重点： **函数内部的 this 只和函数的调用方式有关系，和函数的定义方式没有关系**

- 函数内部的 this 指向谁，取决于函数的调用方式

  - 全局定义的函数直接调用，`this => window`

    ```javascript
    function fn() {
      console.log(this)
    }
    fn()
    // 此时 this 指向 window
    ```

  - 对象内部的方法调用，`this => 调用者`

    ```javascript
    var obj = {
      fn: function () {
        console.log(this)
      }
    }
    obj.fn()
    // 此时 this 指向 obj
    ```

  - 定时器的处理函数，`this => window`

    ```javascript
    setTimeout(function () {
      console.log(this)
    }, 0)
    // 此时定时器处理函数里面的 this 指向 window
    ```

  - 事件处理函数，`this => 事件源`

    ```javascript
    div.onclick = function () {
      console.log(this)
    }
    // 当你点击 div 的时候，this 指向 div
    ```

  - 自调用函数，`this => window`

    ```javascript
    (function () {
      console.log(this)
    })()
    // 此时 this 指向 window
    ```



**call 和 apply 和 bind**

- 刚才我们说过的都是函数的基本调用方式里面的 this 指向
- 我们还有三个可以忽略函数本身的 this 指向转而指向别的地方
- 这三个方法就是 **call** / **apply** / **bind**
- 是强行改变 this 指向的方法



###### call

- `call` 方法是附加在函数调用后面使用，可以忽略函数本身的 this 指向

- 语法： `函数名.call(要改变的 this 指向，要给函数传递的参数1，要给函数传递的参数2， ...)`

  ```javascript
  var obj = { name: 'Jack' }
  function fn(a, b) {
    console.log(this)
    console.log(a)
    console.log(b)
  }
  fn(1, 2)
  fn.call(obj, 1, 2)
  ```

  - `fn()` 的时候，函数内部的 this 指向 window
  - `fn.call(obj, 1, 2)` 的时候，函数内部的 this 就指向了 obj 这个对象
  - 使用 call 方法的时候
    - 会立即执行函数
    - 第一个参数是你要改变的函数内部的 this 指向
    - 第二个参数开始，依次是向函数传递参数



###### apply

- `apply` 方法是附加在函数调用后面使用，可以忽略函数本身的 this 指向

- 语法： `函数名.apply(要改变的 this 指向，[要给函数传递的参数1， 要给函数传递的参数2， ...])`

  ```javascript
  var obj = { name: 'Jack' }
  function fn(a, b) {
    console.log(this)
    console.log(a)
    console.log(b)
  }
  fn(1, 2)
  fn.call(obj, [1, 2])
  ```

  - `fn()` 的时候，函数内部的 this 指向 window
  - `fn.apply(obj, [1, 2])` 的时候，函数内部的 this 就指向了 obj 这个对象
  - 使用 apply 方法的时候
    - 会立即执行函数
    - 第一个参数是你要改变的函数内部的 this 指向
    - 第二个参数是一个 **数组**，数组里面的每一项依次是向函数传递的参数



###### bind

- `bind` 方法是附加在函数调用后面使用，可以忽略函数本身的 this 指向

- 和 call / apply 有一些不一样，就是不会立即执行函数，而是返回一个已经改变了 this 指向的函数

- 语法： `var newFn = 函数名.bind(要改变的 this 指向); newFn(传递参数)`

  ```javascript
  var obj = { name: 'Jack' }
  function fn(a, b) {
    console.log(this)
    console.log(a)
    console.log(b)
  }
  fn(1, 2)
  var newFn = fn.bind(obj)
  newFn(1, 2)
  ```

  - bind 调用的时候，不会执行 fn 这个函数，而是返回一个新的函数
  - 这个新的函数就是一个改变了 this 指向以后的 fn 函数
  - `fn(1, 2)` 的时候 this 指向 window
  - `newFn(1, 2)` 的时候执行的是一个和 fn 一摸一样的函数，只不过里面的 this 指向改成了 obj



##### 17.正则表达式

startfromP108

创建：1.字面量  ；2，内置构造函数

```js
  //1 字面量 //
        var reg = /abc/ 
     //2. 内置构造函数 
        var reg2 = new RegExp("abc")      
        
         console.log(reg.test(mytext.value))
//用reg下的方法test检测，返回T or F  1ab2c3的返回结果为false
```

###### 元字符

**基本元字符**

```js
  		// 1 \d 一位数字（0-9）
        // var reg = /\d\d/
       // 2 \D 一位非数字  \Dk  表示包含一位非数字且为k
        // var reg = /\Dk\D/   

	 // 3. \s 1位空白 （空格 缩进 换行）
 // console.log("12\n3")

  // 4. \S 1位 非空白

  //5 \w 字母 数字 下划线 一位

 //6. \W 非字幕数字下划线 一位

var reg2 = /[a-z]/i
a-z无视大小写


//7  . 任意内容 （换行不算）  常用于 . 以区分任意内容

//8 . \转义字符
        var reg = /\d\.\d/   // 1.2 2.3 
```

###### **边界符**

边界限制

```js
// ^ 开头
        // var reg = /^\d/

// $ 结尾边界
        // var reg = /\d$/

var reg = /^a\dc$/
//开头为a中间为数字结尾为c
```

###### **限定符**

限定字符限定的个数

只能修饰一个 如一个字母或者一个数字（对象）

除非加上()进行整体修饰

```js
 // 1. * 0~多次 
 var reg= /\d*/
//2. + 1~多次
 var reg= /\d+/
 //3. ? 0~1  尽量少非贪婪模式
 var reg=/\d?/
 //4. {n} 指定次数
 var reg=/a{3}/
//4. {n,} >=n  大于等于n次
 
  //5. {n,m}
        var reg=/\d{3,5}/
```

特殊符号

```javascript
// 1.() 整体
        // var reg2= /(abc){2}/
// 2. | 或 ，左右  只分左右
        // var reg = /a|b/
//3 [] 代表1个
        var reg = /[a-w]{3,5}/  //在a-w中的包含3-5次
  //4 [^abc]\

        var reg2 = /[^abc]/  //只要有一个不在abc中的 于开头限定区分kai'lai
        console.log(reg2.test("abz")) //true
```

###### 捕获exec()

```js
 // test()
        // exec() 捕获片段
          // 标识符 g i  g表示全局，就是可以捕获下一个 i代表忽略大小写


        var reg = /(\d{4})-(\d{1,2})-(\d{1,2})/g
             //1.懒惰， 解决 使用全局标识符g

        //2.贪婪

        // var reg = /\d{1,4}/

        // console.log(reg.exec("aa123456bb"))

        //3.非贪婪

        var reg = /\d{1,4}?/
        
        
        var str = `<p class="active"><span>kerwin</span></p>`
        var myreg = /<p.*?>/
        console.log(myreg.exec(str))
```

###### 正则表达式于字符串方法

```js
 <script>
        // 正则.test(字符串)
        // 正则.exec(字符串)

        //字符串.replace  search match

        // var newstr = str.replace("a","*")
        // var newstr = str.replace(/a/g,"*")
        // console.log(newstr)

        //search

        // console.log(str.search("a"))
        // console.log(str.search(/a/))
        // console.log(str.search(/ax/))


        //match 捕获内容
        var datestr = "time is from 2029-01-01 12:20:20 to 2029-11-01 12:20:20"

        // console.log(str.match("ad"))

        console.log(datestr.match(/(\d{4})-(\d{1,2})-(\d{1,2})/g))
		//相比于exec（）一步到位  更加高效
    </script>
```



#### 四. ES6

- 我们所说的 ES5 和 ES6 其实就是在 js 语法的发展过程中的一个版本而已
- ECMAScript 就是 js 的语法
  - 以前的版本没有某些功能
  - 在 ES5 这个版本的时候增加了一些功能
  - 在 ES6 这个版本的时候增加了一些功能
- 因为浏览器是浏览器厂商生产的
  - ECMAScript 发布了新的功能以后，浏览器厂商需要让自己的浏览器支持这些功能
  - 这个过程是需要时间的
  - 所以到现在，基本上大部分浏览器都可以比较完善的支持了
  - 只不过有些浏览器还是不能全部支持
  - 这就出现了兼容性问题
  - 所以我们写代码的时候就要考虑哪些方法是 ES5 或者 ES6 的，看看是不是浏览器都支持

##### let 和 const 关键字

- 我们以前都是使用 `var` 关键字来声明变量的

- 在 ES6 的时候，多了两个关键字 `let` 和 `const`，也是用来声明变量的

- 只不过和 var 有一些区别

  1. `let` 和 `const` 不允许重复声明变量

     ```javascript
     // 使用 var 的时候重复声明变量是没问题的，只不过就是后面会把前面覆盖掉
     var num = 100
     var num = 200
     ```

     ```javascript
     // 使用 let 重复声明变量的时候就会报错了
     let num = 100
     let num = 200 // 这里就会报错了
     ```

     ```javascript
     // 使用 const 重复声明变量的时候就会报错
     const num = 100
     const num = 200 // 这里就会报错了
     ```

  2. `let` 和 `const` 声明的变量不会在预解析的时候解析（也就是没有变量提升）

     ```javascript
     // 因为预解析（变量提升）的原因，在前面是有这个变量的，只不过没有赋值
     console.log(num) // undefined
     var num = 100
     ```

     ```javascript
     // 因为 let 不会进行预解析（变量提升），所以直接报错了
     console.log(num) // undefined
     let num = 100
     ```

     ```javascript
     // 因为 const 不会进行预解析（变量提升），所以直接报错了
     console.log(num) // undefined
     const num = 100
     ```

  3. `let` 和 `const` 声明的变量会被所有代码块限制作用范围

     ```javascript
     // var 声明的变量只有函数能限制其作用域，其他的不能限制
     if (true) {
       var num = 100
     }
     console.log(num) // 100
     ```

     ```javascript
     // let 声明的变量，除了函数可以限制，所有的代码块都可以限制其作用域（if/while/for/...）
     if (true) {
       let num = 100
       console.log(num) // 100
     }
     console.log(num) // 报错
     ```

     ```javascript
     // const 声明的变量，除了函数可以限制，所有的代码块都可以限制其作用域（if/while/for/...）
     if (true) {
       const num = 100
       console.log(num) // 100
     }
     console.log(num) // 报错
     ```

- `let` 和 `const` 的区别

  1. `let` 声明的变量的值可以改变，`const` 声明的变量的值不可以改变

     ```javascript
     let num = 100
     num = 200
     console.log(num) // 200
     ```

     ```javascript
     const num = 100
     num = 200 // 这里就会报错了，因为 const 声明的变量值不可以改变（我们也叫做常量）
     ```

  2. `let` 声明的时候可以不赋值，`const` 声明的时候必须赋值

     ```javascript
     let num
     num = 100
     console.log(num) // 100
     ```

     ```javascript
     const num // 这里就会报错了，因为 const 声明的时候必须赋值
     ```



##### 箭头函数

- 箭头函数是 ES6 里面一个简写函数的语法方式

- 重点： **箭头函数只能简写 函数表达式，不能简写 声明式函数**

  ```javascript
  function fn() {} // 不能简写
  const fun = function () {} // 可以简写
  const obj = {
    fn: function () {} // 可以简写
  }
  
        /*
           1. (只有一个形参的时候)可以省略
           2. {} 可以省略 只有一句代码 或 只有返回值的时候，省略return
  
           3. 没有arguments
  
           4. 箭头函数没有this, 
              箭头函数this是父级作用域的，
        */
  ```

- 语法： `(函数的行参) => { 函数体内要执行的代码 }`

  ```javascript
  const fn = function (a, b) {
    console.log(a)
    console.log(b)
  }
  // 可以使用箭头函数写成
  const fun = (a, b) => {
    console.log(a)
    console.log(b)
  }
  ```

  ```javascript
  const obj = {
    fn: function (a, b) {
      console.log(a)
      console.log(b)
    }
  }
  // 可以使用箭头函数写成
  const obj2 = {
    fn: (a, b) => {
      console.log(a)
      console.log(b)
    }
  }
  ```

  

###### 箭头函数的特殊性

- 箭头函数内部没有 this，箭头函数的 this 是上下文的 this

  ```javascript
  const obj = {
    fn: function () {
      console.log(this)
    },
   
    fun: () => {
      console.log(this)
    }
  }
  
  obj.fn() //object	
  obj.fun()  //window
  ```

  - 按照我们之前的 this 指向来判断，两个都应该指向 obj
  - 但是 fun 因为是箭头函数，所以 this 不指向 obj，而是指向 fun 的外层，就是 window

- 箭头函数内部没有 `arguments` 这个参数集合

  ```javascript
  const obj = {
    fn: function () {
      console.log(arguments)
    },
    fun: () => {
      console.log(arguments)
    }
  }
  obj.fn(1, 2, 3) // 会打印一个伪数组 [1, 2, 3]
  obj.fun(1, 2, 3) // 会直接报错
  ```

- 函数的行参只有一个的时候可以不写 `()` 其余情况必须写

  ```javascript
  const obj = {
    fn: () => {
      console.log('没有参数，必须写小括号')
    },
    fn2: a => {
      console.log('一个行参，可以不写小括号')
    },
    fn3: (a, b) => {
      console.log('两个或两个以上参数，必须写小括号')
    }
  }
  ```

- 函数体只有一行代码的时候，可以不写 `{}` ，并且会自动 return

  ```javascript
  const obj = {
    fn: a => {
      return a + 10
    },
    fun: a => a + 10
  }
  
  console.log(fn(10)) // 20
  console.log(fun(10)) // 20
  ```



##### 函数传递参数的时候的默认值

- 我们在定义函数的时候，有的时候需要一个默认值出现

- 就是当我不传递参数的时候，使用默认值，传递参数了就使用传递的参数

  ```javascript
  function fn(a) {
    a = a || 10
    console.log(a)
  }
  fn()   // 不传递参数的时候，函数内部的 a 就是 10
  fn(20) // 传递了参数 20 的时候，函数内部的 a 就是 20
  ```

  - 在 ES6 中我们可以直接把默认值写在函数的行参位置

  ```javascript
  function fn(a = 10) {
    console.log(a)
  }
  fn()   // 不传递参数的时候，函数内部的 a 就是 10
  fn(20) // 传递了参数 20 的时候，函数内部的 a 就是 20
  ```

  - 这个默认值的方式箭头函数也可以使用

  ```javascript
  const fn = (a = 10) => {
    console.log(a)
  }
  fn()   // 不传递参数的时候，函数内部的 a 就是 10
  fn(20) // 传递了参数 20 的时候，函数内部的 a 就是 20
  ```

  - 注意： **箭头函数如果你需要使用默认值的话，那么一个参数的时候也需要写 （）**



##### 解构赋值

- 解构赋值，就是快速的从对象或者数组中取出成员的一个语法方式



###### 解构对象✅

- 快速的从对象中获取成员

  ```javascript
  // ES5 的方法向得到对象中的成员
  const obj = {
    name: 'Jack',
    age: 18,
    gender: '男'
  }
  
  let name = obj.name
  let age = obj.age
  let gender = obj.gender
  ```

  ```javascript
  // 解构赋值的方式从对象中获取成员
  const obj = {
    name: 'Jack',
    age: 18,
    gender: '男'
  }
  
  // 前面的 {} 表示我要从 obj 这个对象中获取成员了
  // name age gender 都得是 obj 中有的成员
  // obj 必须是一个对象
  let { name, age, gender } = obj
  ```



###### 解构数组

- 快速的从数组中获取成员

  ```javascript
  // ES5 的方式从数组中获取成员
  const arr = ['Jack', 'Rose', 'Tom']
  let a = arr[0]
  let b = arr[1]
  let c = arr[2]
  ```

  ```javascript
  // 使用解构赋值的方式从数组中获取成员
  const arr = ['Jack', 'Rose', 'Tom']
  
  // 前面的 [] 表示要从 arr 这个数组中获取成员了
  // a b c 分别对应这数组中的索引 0 1 2
  // arr 必须是一个数组
  let [a, b, c] = arr
  ```



###### 注意

- `{}` 是专门解构对象使用的
- `[]` 是专门解构数组使用的
- 不能混用



##### 对象简写

```js
   <script>
        mybtn.onclick = function () {
            let username = myusername.value
            let password = mypassword.value

            console.log(username,password)

            var obj = {
                username,
                password
            }

            console.log("发给后端的结构",obj)
        }

        var obj = {
            a:1,
            getName(){
                console.log(this.a)
            }
            //getName:function(){ console.log(this.a) }
        }
        obj.getName()
//当key跟value同名时，可以省略
    </script>
```



##### 模版字符串

- ES5 中我们表示字符串的时候使用 `''` 或者 `""`

- 在 ES6 中，我们还有一个东西可以表示字符串，就是 **``**（反引号）

  ```javascript
  let str = `hello world`
  console.log(typeof str) // string
  ```

- 和单引号好友双引号的区别

  1. 反引号可以换行书写

     ```javascript
     // 这个单引号或者双引号不能换行，换行就会报错了
     let str = 'hello world' 
     
     // 下面这个就报错了
     let str2 = 'hello 
     world'
     ```

     ```javascript
     let str = `
     	hello
     	world
     `
     
     console.log(str) // 是可以使用的
     ```

  2. 反引号可以直接在字符串里面拼接变量

     ```javascript
     // ES5 需要字符串拼接变量的时候
     let num = 100
     let str = 'hello' + num + 'world' + num
     console.log(str) // hello100world100
     
     // 直接写在字符串里面不好使
     let str2 = 'hellonumworldnum'
     console.log(str2) // hellonumworldnum
     ```

     ```javascript
     // 模版字符串拼接变量
     let num = 100
     let str = `hello${num}world${num}`
     console.log(str) // hello100world100
     ```

     - 在 **``** 里面的 `${}` 就是用来书写变量的位置

##### 展开运算符

- ES6 里面号新添加了一个运算符 `...` ，叫做展开运算符

- 作用是把数组展开

  ```javascript
  let arr = [1, 2, 3, 4, 5]
  console.log(...arr) // 1 2 3 4 5
  ```

- 合并数组的时候可以使用

  ```javascript
  let arr = [1, 2, 3, 4]
  let arr2 = [...arr, 5]
  console.log(arr2)
  ```

- 也可以合并对象使用

  ```javascript
  let obj = {
    name: 'Jack',
    age: 18
  }
  let obj2 = {
    ...obj,
    gender: '男'
  }
  console.log(obj2)
  ```

- 在函数传递参数的时候也可以使用

  ```javascript
  let arr = [1, 2, 3]
  function fn(a, b, c) {
    console.log(a)
    console.log(b)
    console.log(c)
  }
  fn(...arr)
  // 等价于 fn(1, 2, 3)
  ```

伪数组转换

  ```js
       // ...伪数组转换

        function test(){
            var arr = [...arguments]
            console.log(arr)
        }
        test(1,2,3,4,5)
  ```





##### 模块化语法

 1.私密不漏 让引入的js私密方法不能被访问	

 2.重名不怕 防止多个js文件引入时的方法同名

 3.依赖不乱 一个js方法引用另一个js方法

###### export/import

在本地浏览中无效，必须存在服务器中✅

