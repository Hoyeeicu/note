[TOC]



## **REM布局**

- px

- em  相对于父元素的字体大小///相对单位

- rem 相对于根元素的字体大小///相对单位

  

### rem自适应fontsize

fontsize=当前设备的css布局宽度/物理分辨率（设计稿的宽度）*基准font-size  

####  小插件 px to rem

改变所有 press F1，enter cssrem 选第一个

html基准font-size不为16px时，设置-->搜索cssrem

![image-20221008181342558](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221008181342558.png)

全选一键改px为rem时注意html中的基准px有没有改为em！！

iconfont也要记得设置为1rem（假如基准px为16px）

## **vh 与vw**

### VW实现fontsize动态变化

    view-height   
       100vh === 视口的高度
    vw view-width 
        100vw ==== 视口高度


        iphone6  100vw  === 375px   1vw = 3.75px
    
        iphone6 plus 100vw === 414px 1vw = 4.14px


        html font-size js代码动态，
    
          font-size=???vw

vw代替js动态设置htmlfontsize

```css
html{
    font-size: 5vw;
    /* 320px=100vw;
    16px=5vw
    vw会随着屏幕大小不断改变，所以fontsize也会不断改变，代替了js的动态fontsize代码 */
}
```

### 100vw与100%的区别

​		width：100vw 包含滚动条，为整个窗口的大小

​		width：100% 不包含滚动条 剩余空间占满

## **css3的特殊属性**

### 渐变

#### **线性渐变**

一个方向向另一个方向渐变

 background:linear-gradient

```css
div{
    width:300px;
    height:300px;
    border:10px solid gray;
    
    background:linear-gradient(red,green,blue)
    /*支持多色渐变
      支持方向，
        background:linear-gradient(to right,red,green)左到右
        background:linear-gradient(to top right,green,blue)右上
      支持角度  background:linear-gradient(78deg,red,green)
        */
}
```

#### 镜像渐变

一个点向四周的颜色渐变

background:radial-gradient

#### -webkit-  增加浏览器兼容性

 background:-webkit-radial-gradient(red,green,blue)

-webkit-  chrome浏览器内核

-moz-    火狐浏览器内核

```css
div{
    width:300px;
    height:300px;
    border:10px solid gray;
    
    background:radial-gradient(red,green,blue)
        /*
        1.布局过度
         background:radial-gradient(red 0%,green 10%,blue 30%)
        0%到10%红绿渐变，10%-30%绿蓝渐变
        2.形状设置
        circle/ellipse
        background:radial-gradient(circle,red,green,blue)
        3.中心点的位置的大小
        background:radial-gradient(60% 40%,closest-side,red,green,blue)
        closest-side渐变到最近的边停止
        farther-side
        close-corner最近的角
        farther-corner
        */
}
```

#### 重复渐变

background:radial-gradient(red,green,blue)

```css
div{
    background:repeat-linear-gradient(red 0%,green 10%,blue 30%)
    background:repeat-radial-gradient(red 0%,green 10%,blue 30%)
}
```

#### 渐变应用：155太极案例

#### 伪元素的使用

### **过渡**

#### 动画过渡属性

！！注意transition放的位置 是在改变前的元素里检测属性改变

过程放慢



transition:  height 2s;

`transition: all 2s linear 3s;`

- all 所有属性 可替换为特定 `transition-property:`
- 2s 动画时间 `transition-duration:`
- linear 匀速 `transition-timing-funtion:`
- 3s 延迟时间  `transition-delay:`
- ！：不支持display：none/block 属性

#### 动画过渡类型  

` transition:all 2s linear; ` 匀速

`transition:all 2s ease;`逐渐慢下来

`transition:all 2s ease-in;`加速

`transition:all 2s ease-out;`减速

`transition:all 2s ease-in-out;`先加速后减速

`transition:all 2s cubic-bezier(.51,1.19,.73,.49);` 贝塞尔曲线		

### **2D变化属性**

#### 2d平移

`translate`

```css
        div{
            width: 200px;
            height: 200px;
            background:red;
            transition:all 2s;
            /* margin: 10px auto; */

            transform: translateX(50px);
            /*相当于position的relative*/
        }
        div:hover{
            /* transform:translateX(100px) translateY(100px); */
        
            transform: translate(100px,100px);
        }
```

###### positon和transform和opacity的区别

![image-20221009133337662](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221009133337662.png)

<img src="https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221009133836741.png" alt="image-20221009133836741" style="zoom: 50%;" />

<img src="https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221009133911142.png" alt="image-20221009133911142" style="zoom:50%;" />

#### 2d-缩放

`scale()`

```css
<style>
        div{
            width: 300px;
            /* height: 300px; */
            border:5px solid red;
            margin:100px auto;
            /* overflow:hidden; */
        }

        img{
            width: 100%;
            transition:all 2s;

            transform-origin:center;
            /* 
              改变中心点的位置
              center /left top /left bottom / left center
              right top/ right bottom/right center
             */
        }
        div:hover img{
            /* width: 150%; */
            transform: scale(1.5);
            /* 负值-倒像放大效果 
                支持x轴 y轴单独放大
                scaleX
                scaleY
            */
            /* transform: scaleY(1.5); */
        }
    </style>
```

#### 2d-旋转

！！Attention：` /* transform: scale(0.5); 缩放后 当动画时会变化为图案原大小*/`

```css
            transform: rotateZ(0deg);

            /* transform-origin: left top; */
            /* 
            rotate 中心 ==== rotateZ
               正值 顺时针
               负值 逆时针
             */

            /* transform: rotateY(0deg); */
            transform-origin: left top;
            /* 
              改变中心点的位置
              center /left top /left bottom / left center
              right top/ right bottom/right center
             改变中心点位置即改变旋转中心点
             */
```

#### 应用P161折扇效果案例

#### 2d-多属性同时设置

```css
        .box div:nth-child(1){
            transform: translateX(400px);
        }
        .box div:nth-child(2){
            transform: translateX(400px) scale(0.5);
        }
        .box div:nth-child(3){
            transform:  scale(0.5) translateX(400px);
        }
/*先位移再旋转或者缩小，不然效果会改变*/
```

#### 2d-倾斜

```css
            /* transform: skewY(30deg); */

            transform: skew(30deg,30deg);

            /* skewX 正值， 拽右下角， 往右边拉动， 形成30deg
            skewY
            skew(x,y) 正值， 拽右下角， 往右下边拉动， 形成30deg*/
        }
```

#### **明星资料卡案例**

### **关键帧动画**

###### amimation和transition的区别

<img src="https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221009151228539.png" alt="image-20221009151228539"  />

##### 关键帧动画属性

```css
<style>
        div{
            width: 200px;
            height: 200px;
            background:red;
            animation: kerwinrun1 2s linear infinite;
            /* infinite 无限次 */
        }
        /* 声明动画，两种方式 */
        @keyframes kerwinrun1 {
            from{
                width: 200px;
                height: 200px;
                background:red;
            }

            to{
                width: 400px;
                height: 600px;
                background:green;
            }
        }
        @keyframes kerwinrun2 {
            0%{
                width: 200px;
                height: 200px;
                background:red;
            }
            25%{
                width: 200px;
                height: 400px;
                background:yellow;
            }
            50%{
                width: 400px;
                height: 400px;
                background:blue;
            }
            75%{
                width: 400px;
                height: 500px;
                background:gray;
            }
            100%{
                width: 400px;
                height: 600px;
                background:green;
            }
        }
    </style>
```

##### 关键帧动画单个属性分析

- animation-name
- animation-duration
- animation-funtion
- animation-delay
- animation-iteration-count
- animation-direction

![image-20221010141541179](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010141541179.png)

![image-20221010141501898](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010141501898.png)

![image-20221010141705909](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010141705909.png)

###### 画面定格

animation-fill-mode

```css
        div{
            height: 100%;
            width: 200px;
            background:red;
            position: fixed;
            left:0px;
            top:0px;

            transform: translateX(-100%);
            /* 100% 是相对于自身的100% */
            
            /* animation: run 1s linear forwards; */
            animation: run 1s linear forwards reverse;
            
            /* animation-fill-mode: forwards; */
            /* none 默认值          
               forwards 最后的画面
               backwards 初始画面
             */
        }
```

##### **关键帧动画轮播案例**

##### **关键帧动画，逐帧动画案例**

###### animation-timing-function的属性 steps

```css
{  <!-- steps(直接进行关键帧跳跃)  , linear ,ease-in  !-->
        /* animation: run 5s steps(1,start); */
            /* animation: run 5s step-start; */
            animation: run 5s step-end;

            /* end（保留当前帧，看不到最后一帧，动画结束） */
            /* start（保留下一帧，看不到第一帧，从第一帧很快跳到最后一帧） */
        }
```

#### **Animate动画库**

### **3d动画**

#### transform-style：preserve-3d

- flat  2D 默认
- preserve-3d   3D

##### 3d位移

  /* transform:translateZ(-200px); */

###### 景深perspective

![image-20221010170333522](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010170333522.png)

不设置默认最远，即Z轴移动时大小不变

##### 3d旋转

```css
        .center{
            margin:auto;
            width: 200px;
            height: 200px;
            background:red;

            /* transform: rotateX(30deg); */
        
            /* transform: rotateY(30deg);
             */

             /* transform: rotateZ(30deg); */


             transform: rotate3d(0,0,1,30deg);

             /* 前面三个值取值 0-1 */
        }
```

##### 3d缩放

```css
            /* transform: scaleZ(10) rotateX(45deg); */
            transform: scale3d(1,1,10) rotateX(45deg);
```

![image-20221010172441574](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010172441574.png)

##### **3d-立方体案例**

### **网格布局**grid

```css
    <style>
        .box{
            width: 200px;
            height: 200px;
            background:red;
            /* display: grid; 块级网格 */
            /* display: inline-grid; 行内块级网格 */

            display: grid;
        }
    </style>
```

##### 行列分布

```css
    <style>
        div.box{
            width: 600px;
            height: 600px;
            border:5px solid gray;
            display: grid;

            /* 1 固定值 */
            /* grid-template-rows: 200px 200px  200px;
            grid-template-columns: 200px 200px  200px; */

            /* 2 百分比 */
            /* grid-template-rows: 33.3% 33.3% 33.4% ;
            grid-template-columns: 33.3% 33.3% 33.4% ; */

            /* 3 repeat */
            /* grid-template-rows: repeat(3,33.33%);
            grid-template-columns: repeat(3,33.33%); */

            /* 4. repeate autofill */
            /* grid-template-rows: repeat(auto-fill,200px);
            grid-template-columns: repeat(auto-fill,20%); */
        
            /* 5. fr 片段 */
            /* grid-template-rows: 1fr 2fr  1fr;
            grid-template-columns: 1fr 2fr  1fr; */
        
            /* 6. minmax */
            /* grid-template-rows: minmax(100px,200px)  200px 100px;
            grid-template-columns: 200px  200px 200px; */

            /* 7 auto */

            grid-template-rows: 100px  200px auto;
            grid-template-columns: 100px  200px auto;
        }
```

##### 行列间距

```css
            row-gap:20px;
            column-gap:20px;
            gap:20px 20px;
```

##### 网格区域命名与合并

先把区域名字弄成相同的，后再让指定的孩子占满某个区域（根据区域名字）

```css
         {   grid-template-columns: 200px 200px 200px;
            grid-template-rows: 200px 200px 200px;

            grid-template-areas: 'a e e'
                                 'd e e'
                                 'g h i' 
            ;
        }
        /* .box div:nth-child(1){
            grid-area:a;
        } */

        /* .box div:nth-child(5){
            grid-area:e;
        } */

        .box div:nth-child(2){
            grid-area:e;
        }
```

##### **网格布局案例1**

##### 网格布局的对齐方式

###### 改变网格顺序

/* grid-auto-flow: column; 改变顺序 */默认是rowg

###### 改变网格位置

`justify-content: center/space-between/space-around/star/end;`

`align-content: center/space-between/space-around/star/end;` 

 简写`*place-content*: center center;`

###### 项目再容器中的位置

justify-items:

align-items:

place-items:

![image-20221010203547094](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010203547094.png)

##### 网格布局的项目属性

![image-20221010203902476](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010203902476.png)

![image-20221010204629433](https://raw.githubusercontent.com/Hoyeeicu/note-blog/main/img/image-20221010204629433.png)

```css
   
        .box div:nth-child(2){
            /* grid-column-start:2;
            grid-column-end:4;

            grid-row-start:1;
            grid-row-end:3 */

            grid-column: 2/4;
            grid-row:1/3;
		}
```



##### 网格布局案例2



















