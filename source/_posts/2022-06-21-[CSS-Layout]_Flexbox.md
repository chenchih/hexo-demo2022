---
title: CSS LAYOUT - Flexbox
date: 2022-06-21 20:33:42
tags:
- Frontend
- CSS
categories:
- [WebDev, CSS]
---
# Flex Layout 排版 (CSS 格線佈局)

CSS排版有很多不同的排版工具，今天我想介紹FlexBox，也可以叫做flexible。Flexbox 是屬於one dimention ，也就去說你只有一個軸，你不是選擇用row or colomn。我會介紹以下的內容：
- 父元素/容器属性：
    - flex-direction: 
        - row (default)
        - row-reverse 
        - column
        - column-reverse
    - flex container(display): 
        - flex 
        - inline-flex
    - flex-wrap: 
        - wrap
        - nowrap (default)
    - justify-content
        - flex-start
        - flex-end
        - center
        - space-around
        - space-between
        - space-evenly
    - align-item
        - stretch
        - lex-start
        - flex-end
        - center
    - Align-Content
        - flex-start
        - flex-end
        - stretch
        - space-around
        - space-between
- Flex 內元件屬性/子元素：
    - flex-item:
        - flex-grow
        - flex-shrink
        - flex-basis
        - flex (縮寫)
    - order
    - align-self

## part 1 基本FLEX相關知識
FlexBox 就是flexible Box，顧名思義就是彈性的盒子。早期我們在排版都是用float，但用起來沒有FlexBox好用。我們有幾個CSS layout，如`float`,`display`,`Positioning`, `Flexbox`, and `grid`等等。

### Container and items 的差別
- **`Container`:** 就是`外容器`，你也可以想成它是盒子的外面，或是我喜歡稱他為Parent容器。
- **`Items`:** 就是`內容器`，你也可以想成它是盒子的裡面，或是我喜歡稱他為Child容器。
我們來看一下圖你們更了解，這兩個差別:外面綠色就是container(外容器)，裡面橘色就是items()內容器)

![](https://i.imgur.com/zqn2Yrl.png)

這非常重要，這樣你才知道要用那一個容器的元屬性，然後也很好去記，卻步用去蓓背他。

### AXIS軸
Flexbox 具有主軸起點、終點、尺寸與交錯軸起點、終點、尺寸的特性可以進行布局規畫。

我要在這裡介紹`main-axis`主軸(`水平Horizontal`)和 `cross-axis`交錯軸(`垂直vertical`)。

 - `main-axis主軸`: 就是走X方向或是水平(Horizontal)，這是他預設的，因為`flex-direction`預設是`row`，因此它是走右到左(起點:右，終點:左)。如果你想改成走垂直vertical，也是可以，就把`flex-direction`改`coloumn`，就會有上到下(起點:上，終點:下)。它會用屬性`justify-content`。

 - `cross-axis交錯軸`: 就是走Y方向或是走`垂直vertical`。它會用屬性`align-items`,和 `align-content`。

![](https://i.imgur.com/TL4nzzR.png)

![](https://i.imgur.com/Vz8M4ne.png)

這張圖應蓋更清除了，預設main是水平，如果你要走垂直，請看圖的`column`，`main`的軸就改了。
![](https://i.imgur.com/x9TMxYR.png)

## Part 2 Parent 外容器

### 1. display
一開始要宣告為 `flex` 才能使用，如果沒有宣告為 flex，無法作用。還有一個 `inline-flex`，作用類似於 `inline-block + flex`

> 指令: `display: {flex |inline-flex}`

| 屬性值properties | 說明 Description|
| -- | -- |
|  flex  | 如果沒有設定寬高，它跟block 一樣佔據了整行 |
| inline-flex  |就是inline-block + flex，如果沒有設定寬高，它只會用他有擁有的空間。|



- 下面圖會更請楚

![](https://i.imgur.com/OKWpLtk.png)

-  <font size=5> flexbox 比較看看</font>
![](https://i.imgur.com/jYLlPft.png)

 <font size=5> **Example**</font>
![](https://i.imgur.com/f2p0vxd.png)

**<font color="red">補充 inline VS Block</font>**

- `inline`:
  - **無法**透過 `width` 與 `height` 屬性調整寬高。
  - 寬高取決於內容(例如文字)的長度與行高(line height)。
  - 呈現水平排列。

- `block`:
  - 預設寬度為容器的 100%。
  - 可以透過 `width` 與 `height` 屬性調整寬高。
  - 強迫換行，呈現垂直排列。

- `inline-block`:
  - 把`inline` 和` block` 結合再一起。
  - 可以透過 `width` 與 `height` 屬性調整寬高。
  - 呈現水平排列。
  - 在無設定 width 與 height 時，寬高由內容決定。
![](https://i.imgur.com/yqyRL3t.png)


 <font size=3>  **Reference:** [inline-block](https://ithelp.ithome.com.tw/articles/10219161)</font>


### 2. justify-content 屬性介紹(main axis)
主要以主軸線`main-axis`來排版(`main axis`)
> 指令: justify-content: {flex-start| flex-end | center| space-around| space-between | space-evenly}

| 屬性值properties | 說明 Description|
| -- | -- |
| flex-start  | 預設值/默認值，對齊主軸線最前端 |
| flex-end | 對齊主軸線最終端 |
| center  | 對齊主軸線中央 |
| space-around  | 平均分配寬度和間距，第一項和最後一項比較短 |
| space-between  |平均分配寬度，第一項和最後一項貼齊邊緣 |
| space-evenly  | 平均分配寬度和間距 |

#### Example
 ![](https://i.imgur.com/qHvQcXv.png)

 -  space-around vs space-evenly
 ![](https://i.imgur.com/e2slCFW.png)

- main-axis 水平和垂直
![](https://i.imgur.com/LGqENxP.png)



### 3. align-items 屬性介紹 (cross-axis)
主要以`交錯軸線cross-axis`來做排版
> 指令: `align-items: {flex-start| flex-end | center| stretch| baseline}`

| 屬性值properties | 說明 Description|
| -- | -- |
| stretch  | 預設值/默認值，將內容元素撐開至 flexbox 大小 |
| flex-start  | 對齊交錯軸線最前端 |
| flex-end |對齊交錯軸線最末端|
| center  | 對齊主軸線中央 |
| baseline  | 對齊內容物的基線 |

![](https://i.imgur.com/btlBsMd.png)

#### Example
![](https://i.imgur.com/1aAHxy7.png)

<font color="red" size=3> 總結 justify-content and align-items </font>


![](https://i.imgur.com/7IDuNrN.png)

![](https://i.imgur.com/RmgOZkt.png)

### 4. align-content 屬性介紹
跟`align-items` 相同差別在於多行，`align-items 單行`
> 指令: `align-content: {flex-start| flex-end | center| stretch| baseline}`

| 屬性值properties | 說明 Description|
| -- | -- |
| stretch  | 預設值/默認值，將內容元素撐開至 flexbox 大小 |
| flex-start  | 對齊交錯軸線最前端 |
| flex-end |對齊交錯軸線最末端|
| center  | 對齊主軸線中央 |
| baseline  | 對齊內容物的基線 |

![](https://i.imgur.com/KMi7Ic6.png)

#### Example
![](https://i.imgur.com/N4CJ71n.png)

#### align-item vs align-content 比較
我們可以看到，如果用個是align-content 再把螢幕縮小，它會換到下一行。
可是用同樣方法，我們改成align-items，它就不會換新行會重新排。
![](https://i.imgur.com/kATWvxj.png)

### 5.flex-direction 屬性介紹
<font color="red">這是決定我們主軸方向(main and cross)。</font>
container 加了 display: flex;屬性時，內容物會依照交錯軸線排列成一行，如果我們想將內容物呈現直向排列，可以透過 flex-direction 來設定。row ->橫向排列，column直向排列

> 指令: `flex-direction:{ row|row-reverse|column|column-reverse}`

| 屬性值properties | 說明 Description|
| -- | -- |
| row  | 預設值/默認值，內容物依照主軸線(main-axis)，橫向排列(左至右) |
| row-reverse  | 與row相同，且主軸線起點與終點相反((右至左)) |
| column |交錯軸線位置與主軸線(cross-axis)，直向排列(上至下)|
| column-reverse  | 與column相同，且主軸線起點與終點相反(下至上) |


![](https://i.imgur.com/fDSkBRc.png)

#### Example
![](https://i.imgur.com/UL2XdxE.png)

### 6.flex-wrap 屬性介紹
- 超出範圍時是否換行的屬性，分為換行、不換行、換行時反轉
- 如果子元素數量較多時，內容常會被壓縮且擠在同一行，這時我們就可以透過 flex-wrap 來換行。

> 指令:`flex-wrap:{nowrap | wrap | wrap-reverse}`

| 屬性值properties | 說明 Description|
| -- | -- |
| nowrap  | 預設值，不斷行 |
| wrap  |   沒空間，就換行，第一行在上方，(column:第一行，就往右) |
| wrap-reverse| 沒空間，就換行(wrap 相反))，第一行在下方，(column:第一行，就往左)|

![](https://i.imgur.com/TyxiMzb.png)

#### Example
- `ROW(default)`
![](https://i.imgur.com/5ie4wbS.png)

- `column`
![](https://i.imgur.com/eoQyBLu.png)


### 7. Flex-flow縮寫
- 它是`flex-direction` 和`flex-wrap`的縮寫。
> 指令:`flex-flow:{flex-direction |flex-wrap}`

## Part 3 Items Properties (Child)內元件

接下來我們要開始了解內元件 也就是`items`。有了上面的`container`，接下來我們要來介紹如何設定裡面的盒子。

### 1. order
可以重新定義元件的`排列順序`，順序會依據數值的大小排列。

> 指令:`order: ｛<integer>｝` /* default ０ */

- `order`直的數字越大排越後面，越小越前面，包括-1
![](https://i.imgur.com/X9sCtSW.png)

#### Example 
![](https://i.imgur.com/0qjnWVf.png)


### 2. grow
- 子元素「`伸展`」比例分配：數字，無單位，`預設值為 0`，不可為負值
- 尚未進行設定時(`預設值`)，不會將剩餘空間分配給子元素做長度「`伸展`」，設定為 1 長度會進行彈性變化。分配的比例會依照設定的數值進行配置
> 指令:flex-grow: {<number>} /* default 0 */

![](https://i.imgur.com/1B4Gj4K.png)


- `預設為0`。因此他不會伸展，如果你把其中子元素改成1，只有那一個`子元素item`就會如果。如果改`2個子元素items`他們會`平均分配`。

#### Example
我們可以看到item6 設grow為1，只有它會伸展，但如果我們設兩個item 為grow=1，它們會平均伸展
![](https://i.imgur.com/X9sCtSW.png)


### 3. shrink
- `items子元素`「`shrink 壓縮`」比例分配：數字，無單位，`預設值為 1`，不可為負值伸展，
- 尚未進行設定時(預設值)，會按照數字「`shrink壓縮`」比例分配。如果不想要被壓縮的話，可以設定數值為 `0`。

> 指令:`flex-shrink: {<number>}` /* default 1 */

![](https://i.imgur.com/cj8v7Xw.png)
我們看上面圖，所有子元素都是為1(預設)，只有第2個子`元素為0`，換句話說，如果空間不足，所有子元素都會被壓縮

#### Example
![](https://i.imgur.com/9iugTtJ.png)


### 4. basis
 子元素基本大小：預設值為 auto。其實它可以設為跟width或height屬性一樣的。

> 指令:`flex-basis: {}<length>} | auto; ` /* default auto */

#### basis VS width 優先順序

![](https://i.imgur.com/3XYd1es.png)

### 5. flex 縮寫(grow shrink basis)
> 指令:`flex-wrap:{grow | shrink | basis}`

| 屬性值properties | 說明 Description|
| -- | -- |
| nowrap  | 伸展性，是一個數值，當空間分配還有剩餘時的當前元件的伸展性，預設值為 0，如果設置為 0 則不會縮放 |
| flex-shrink |   元件的伸展性，是一個數值，當空間分配還不足時的當前元件的收縮性，預設值為 1，如果設置為 0 則不會縮放。 |
| flex-basis| 元件的基準值，可使用不同的單位值 |

**不同寫法:**
```
flex: 0 1 auto /* default */
   or <flex-grow> <flex-shrink> <flex-basis>
   or <flex-grow>
   or <flex-basis>
   or <flex-grow> <flex-basis>
   or <flex-grow> <flex-shrink>
```

![](https://i.imgur.com/nbUJouX.png)

#### Example
![](https://i.imgur.com/5zmMVYA.png)

### 6.align-self
`align-self` 可以個別調整`items子元素`在`cross-axis交錯軸線`的位置。它會覆蓋父元素上設定 `align-item`

> 指令: `align-self: {auto | flex-start | flex-end | center | baseline | stretch}`

- `Auto` 就是指`父元素container`上設定 `align-item`。也就是如果你沒有設`align-self`，就會用父元素上設定 align-item。
- 假如我們已經在父元素上設定 align-item，但要其中一個內容物的位置需要調整成其他對齊方式，這時我們就可以針對該元素設定 `align-self` 來覆寫原本 `align-item` 的屬性。

![](https://i.imgur.com/HBU0f9l.png)

#### Example
![](https://i.imgur.com/XKMVy6g.png)

## 總結
![](https://i.imgur.com/mI98jsY.png)

### Row
![](https://i.imgur.com/BHVm0G3.png)

### column
![](https://i.imgur.com/VWmtJrr.png)


## Reference:
- http://tsweb44.com/TS_HTML5CSS3_4/TSwrite/i12.html
- https://www.casper.tw/css/2017/07/21/css-flex/#Flex-%E7%9A%84%E5%A4%96%E5%AE%B9%E5%99%A8%E8%88%87%E5%85%A7%E5%85%83%E4%BB%B6
- https://w3c.hexschool.com/flexbox/2186a786
- https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html
- https://iq.opengenus.org/types-of-css-layout/
- https://angrytools.com/css-flex/
- https://blog.csdn.net/mwl_learning/article/details/115443138?spm=1001.2014.3001.5502

## FlexBox Example
- ### Example1: Basic Nav Bar

#### HTML
```
<body>
    <nav>
      <ul>
        <li>Home</li>
        <li>About</li>
        <li>Service</li>
        <li>Contact</li>
      </ul>
    </nav>        
</body>
```
#### CSS
```
nav{
    font-size: 2rem;
    background-color: #f1f1f1;

  }

  nav ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    display:flex;
    /* justify-content: space-around; */
  }

  nav ul li{
    cursor: pointer;
    padding: 0.5rem;
    flex: auto;
    text-align: center;

  }

  nav ul li:hover {
   background-color: #555;
  color: white;
  }

  @media all and (max-width:400px){
    nav ul {
      flex-direction: column;    
  }
    nav ul li {
    text-align: center;  
  }

  }
```
#### OUTPUT
![](https://i.imgur.com/inl7Dn4.png)

---
### Example2
#### html
```
<body>
<header class="flex-header">
  HEADER
</header>
<main class="flex-main">
  <nav class="flex-nav">
    SIDEBAR
  </nav>
  <article class="flex-article">
    MAIN CONTENT
  </article>
  <aside class="flex-aside">
    SIDEBAR
  </aside>
</main>
<footer class="flex-footer">
Footer
</footer>
</body>
```

#### CSS
``` *{
  margin: 2px;
  }
body{
    font-size:24px;
    color: white;
    height: 550px; /*100vh*/
    text-align:center;
    display: flex;
    flex-direction: column;
  }

  .flex-header{
    background-color: #5070b5;
    padding-top: 3rem;
    padding-bottom: 3rem;
  }
  .flex-main{
    display: flex;
    flex: 1 ;
  }
  .flex-nav{
    background-color: #B95F21;
    padding-top: 3rem;
    flex: 1 1 5rem;
  }
  .flex-article{
    background-color: #81a43c;
    padding-top: 3rem;
    flex: 3 3;
  }
  .flex-aside{
    background-color: #b95f21;
    padding-top: 3rem;
    flex: 1 1 5rem;
  }
  .flex-footer{
    background-color: #5070b5;
    padding-top: 3rem;
    padding-bottom: 3rem;
  }
  @media all and (max-width: 500px){
    .flex-main{
        flex-direction: column;
    }
  }
```
#### OUTPUT
![](https://i.imgur.com/9svjArI.png)

---

### Example3
#### HTML
```
<body>
 <h1> Hello World </h1>

 <div class="container">
    <img src="https://static.pexels.com/photos/52500/horse-herd-fog-nature-52500.jpeg" alt="">
    <img src="https://static.pexels.com/photos/66898/elephant-cub-tsavo-kenya-66898.jpeg" alt="">
    <img src="https://static.pexels.com/photos/213399/pexels-photo-213399.jpeg" alt="">
    <img src="https://static.pexels.com/photos/158471/ibis-bird-red-animals-158471.jpeg" alt="">
    <img src="https://static.pexels.com/photos/133459/pexels-photo-133459.jpeg" alt="">
    <img src="https://static.pexels.com/photos/50988/ape-berber-monkeys-mammal-affchen-50988.jpeg" alt="">
 </div>
</body>
```

#### CSS
```
.container{
display: flex;
flex-wrap: wrap;
justify-content: center;
}
h1{
font-family: fantasy;
font-size: 3em;
border-bottom: 5px solid red;
border-right: 5px solid darkgreen;
width:400px;
text-align: center;
}
img{
height: 400px;
height: 300px;
margin: 10px;
}
```

#### OUTPUT

![](https://i.imgur.com/zkYr6lS.png)


---

### Example4
#### HTML
```
<body>
  <nav class="navbar">
    <div class="container">
      <div class="logo">Flexbox</div>
      <ul class="nav">
        <li>
          <a href="#">Home</a>
        </li>
        <li>
          <a href="#">About</a>
        </li>
        <li>
          <a href="#">Contact</a>
        </li>
      </ul>
    </div>
  </nav>
  <header class="header">
    <div class="container">
      <div>
        <h1>Flexbox Crash Course</h1>
        <p>
          This crash course was created by Brad Traversy to help you learn the
          basics of flexbox. Flexbox is a very important and useful tool in
          CSS.
        </p>
      </div>
      <img src="grid.svg" alt="" />
    </div>
  </header>
  <section class="boxes">
    <div class="container">
      <div class="box">
        <h2><i class="fas fa-arrows-alt-v"></i> Alignment & Space</h2>
        <p>
          A more efficient way to lay out, align and distribute space among
          items in a container
        </p>
      </div>

      <div class="box">
        <h2><i class="fas fa-arrows-alt"></i>Tricky Positioning</h2>
        <p>
          Flexbox usually solves tricky problems including how to position or
          dynamically resize elements on a page
        </p>
      </div>
      <div class="box">
        <h2><i class="fas fa-mobile"></i>Responsive Design</h2>
        <p>
          Flexbox makes building a website layout (and making it responsive!)
          much, much easier
        </p>
      </div>
    </div>
  </section>
</body>
```
#### CSS

  ```
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');
  *{
      box-sizing: border-box;
      margin: 0;
      padding: 0;
  }
  body{
  font-family: 'Poppins', sans-serif;
  font-size: 16px;
  line-height: 1.5;
  color: #333;
  background-color: #a1c3ff;
  }
  img{
  max-width: 100%;
  }
  h1,
  h2 {
      margin-bottom: 15px;
  }
  ul {
  list-style: none;
  }
  .container{
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 30px;
  }
  .navbar{
      background-color: #3474e6;
      color: 60px;
      height: 60px;
  }
  .navbar .logo {
  font-size: x-large;
  font-weight: bold;
  }
  .navbar a{
  color: #fff;
  text-decoration: none;
  font-size: 18px;
  font-weight: bold;
  }
  .navbar a:hover{
      color: lightblue
  }
  .navbar .container{
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
  }
  .navbar ul {
      display: flex;
  }
  .navbar ul li {
      margin-left: 20px;
  }
  header{
  background-color: #0151cc;
  color: white;
  min-height: 400px;
  }
  .header h1{
  font-size: 3rem;
  font-weight: bold;
  line-height: 1.2;  
  }
  .header img{
  max-width: 400px;
  }
  .header .container {
      display: flex;
      align-items: center;
      justify-content: space-between ;
  }
  .boxes .container {
      display: flex;
      justify-content: space-between;
  }
  .box {
      flex:1;
      background-color: #0a51cc;
      color: white;
      border-radius: 10px;
      margin: 20px 10px;
      box-shadow: 0 3px 5px rgba(0, 0 , 0, 0.6);
      padding: 15px 20px;
  }
  .box i {
      margin-right: 10px;
  }

  @media(max-width: 768px) {
      .header .container{
          flex-direction:column;
          padding-top: 20px;
          text-align: center;
      }
      .boxes .container {
          display: block;
          text-align: center;
      }
  }
  ```
#### OUTPUT
![](https://i.imgur.com/kTwt6xv.png)
