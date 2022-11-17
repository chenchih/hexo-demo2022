---
title: CSS LAYOUT - GRID 介紹
date: 2022-06-11 09:52:52
tags:
- Frontend
- CSS
categories:
- [WebDev, CSS]

---
# GRID Layout 排版 (CSS 格線佈局)

- 現在我們在做網頁排版，最流行都是用 `GRID` and `Flex`。想要分享`GRID`相關設定和用法，在早期都是用`position` 或`float`等等來做排版。
- `GRID` 是二維CSS格線排版(row `and` colulmn)，反之`Flex`只能選用一維(row `or` colulmn)。
---
> 以下是所有<font color="red">`GRID` Properties </font>，我整理好分類，這樣才懂或記。如果有學會或用過`GRID`，會更好理解。


- Grid Container(parent Properties)
    - 1.display (enable grid propertis 啟動GRID)
	- 2.grid-template
	  - grid-template-column 
	  - grid-template-row 
	  - grid-template
	  - grid-template-areas
    - 3.grid-auto-flow
	  - grid-auto-column
	  - grid-auto-rows
	  - grid-auto-flow 	    
	- 4.gap 
	  - column-gap
	  - row-gap
	  - gap
	- 5.Alignment & Spacing
		- within grid cell
			- justify-items
			- align-items
			- place-items 
		- within grid container
			- justify-content
			- align-content
			- place-content
- Grid item(Child Properties)
	- Grid-column-start
	- Grid-column-end
	- Grid-row-start
	- Grid-row-end
	- Grid-column (shorthand)
	- Grid-row (shorthand)
- Alignment item within Cell
	- Justify-self: alignment along the row axis
	- Align-self: alignment along the column axis
	- Place-self: shorthand for <align-self> <justify-self>
	
---

## Part 1: GRID 架構 Structure & Terminology
### Container 和 Items 差別：
> `Grid Container`: 盒子的最外層Parent 
> `Grid items`: 盒子內層Children 
> 其實跟Flex一樣，都需要有container and items

![container and items of GRID](https://i.imgur.com/g882pUK.png)

### 專有名詞Terms

| 名詞 | 說明 Description|圖示|
| -- | -- | -- |
| Grid line |  Grid的線條之間。Horizontal or Vertical divided line in a grid ||
| Grid Cell  |intersection of the grid. grid 的最小單位||
| Grid-Area  |||
|Grid-Track|格線軌道，兩條線之間的區域。||
| explicit-track  |透過 `grid-template-columns` 與 `grid-template-rows`|虛線（dashed line）|
| implicit-track  |透過 `grid-auto-rows` 和 `grid-auto-columns`|點線（dotted line）|
|Gap|可以透過 `column-gap`, `row-gap`, 或簡寫的 `gap` 來定義。|斜虛線（diagonal dashed line）|

![terms](https://i.imgur.com/eYFvrl5.png)

#### Grid Track 
我想分享一下Grid Track 類似相關設定。我們有分兩種Grid Track，請看下面圖更了解他們的差別。我們可以用線來區分它們的差別

>`explicit-track`: 透過 `grid-template-columns` 與 `grid-template-rows`，以虛線（dashed line）
> `implicit track`: 透過 `grid-auto-rows` 和 `grid-auto-columns` ，以	點線（dotted line）

![](https://www.quackit.com/pix/stock/css_grid_explicit_and_implicit_track_sizing.png)

##### Example:
![](https://i.imgur.com/inHY2cJ.png)

#### Grid GAP
spaces between each column/row are called gaps. 欄或列之間的空見。我下面有介紹如何用。

> gap: 可以透過 `column-gap`, `row-gap`, 或簡寫的 `gap` 來定義。|斜虛線（diagonal dashed line）

![](https://i.imgur.com/6dKkLZx.png)

### GRID程式碼範例 Grid Sample Code 
- 以下會用到的HTML and CSS程式碼範例。Example Code for demo on different properties
![](https://i.imgur.com/a9h6p6F.png)

- HTML:
```
<body>
    <div class="container"> 
        <div class="grid-item item-1">Item 1</div>
        <div class="grid-item item-2">Item 2</div>
        <div class="grid-item item-3">Item 3</div>
        <div class="grid-item item-4">Item 4</div>
        <div class="grid-item item-5">Item 5</div>
        <div class="grid-item item-6">Item 6</div>
        <div class="grid-item item-7">Item 7</div>
        <div class="grid-item item-8">Item 8</div>
        <div class="grid-item item-9">Item 9</div>
    </div>
</body>
```

- CSS:
```
*{
    margin: 0px;
    padding: 0px;
}

.container{
display: grid ;
border: 6px solid black;
}

.grid-item{
color: #000;
font-size: 1.5rem;
padding: 1rem;
text-align: center;
}

.item-1{
    background-color: red;
}
.item-2{
    background-color: yellow;
}
.item-3{ 
    background-color: lightgreen;
}
.item-4{
    background-color: pink;
}
.item-5{
    background-color: skyblue;
}
.item-6{
    background-color: greenyellow;
}
.item-7{
    background-color: green;    
}
.item-8{
    background-color: blue;
}
.item-9{
    background-color: orange;
}
```

## Part 2-1: Grid Container(parent Properties)
以下我開使介紹Container 和 Items相關　properties。

### 1. display
By `default` the content has created single column grid for the items. All of the grid items lay in `row`, which behave like `block element`, so this is why even if you don\'t add `display: grid` the content will lay block. If you  `don't` wants grid container to `display in block`, you can change it to `inline-block`. There are two properties for display as below:  

>  Display properties : `<grid>` or `<inline-grid>`
>> `display: grid` : default items lay in row and stretch behave to block element 
>> `dispplay: inline-grid`: will not display in block element 

#### Example of the display properties
```
.container{
display: grid ; //or inline-grid
border: 6px solid black;
}
```

![](https://i.imgur.com/3golNqE.png)

### 2. grid-template: set rows or colulmns  
We have three properties: 
 > - `grid-template-row` : set how many rows 設定列
 > - `grid-template-column` set how many column 設定欄
 > - `grid-template` shortcut for row and column 列與欄的縮寫

以下是設他不同的值(value)的方法 Below are setting value option:
>- non-negative length value like 任何正數 `px`, `%` , `rem`等等
>- `auto`: determined by the size of the container, and on the size of the content of the items。尺寸是以照內容的寬度呈現
>- `fr`: 就是fraction ，指的是 container扣掉 grid-gap `後的空間加以分配`，用法類似 `flex-grow` 和 `flex-shrink`。 Fraction will take free space avaiable of the container anf gap space , which is related to `flex-grow` 和 `flex-shrink` 
![](https://i.imgur.com/jConRyo.png)
>- `repeat()`可重複 and `minmax()`可將值限定在某區間，傳入兩個參數，最小值與最大值
> - `auto-fit` and `auto-fill`: 自動重複網格線(自動填滿網格軌道)
> -　`fit-content` 貼合內容尺寸貼合內容尺寸

#### grid-template-columns (column width - 欄的寬度)
Specifies number of columns in a grid layout, each value represent the size of column; the `width of items`. Column also refer to Y axis vertical axis. 

> **Syntax**: `grid-template-columns: size` 
>> `1 column` =>　`grid-template-columns: 100px;`
>> `3 column` =>　`grid-template-columns: 100px 100px 300px;`
>> the more value you enter the more column will set

![](https://i.imgur.com/bgApvOe.png)

- ##### value as `PX` or `auto` 
> - 設定寬度大小以`px`為單位，或 `auto`。
    > - 如果設用寬度大小為`auto`就是內容，會把它展最大寬度。請看我下面圖。We can also set other than px or auto, auto will stretch to max width
    > - 如果設定單一值(value)，就是`1欄`，以我的圖設`3個px` 說明3欄。Value can set with `1 parameter size(for one colulmn)`, set `3 parameter size (for 3 column)`
     
    - **EX1**(自訂不同欄的寬度):
    > `grid-template-columns:100px 200px 300px` 

    - **Ex2**: 我們也可以用`auto` 自動調寬度大小，如下面:
    >`grid-template-columns: auto auto auto;`

    ![](https://i.imgur.com/8txVTrW.png)


It will create three column, `first column is 100px`, `second is 200px`, and `third is 300px`. Since we define three column, so the forth items will be in second row. 
以上面的例子我們設3個PX就說明3欄，所以第4欄就換行就變成第2列。

- ##### value as `repeat()` 
    > - 如果有`同樣的大小`，我們可以用`repeat`這個函數，如下面例子。 We can also use the `repeat` option, to set all column with the same width, pelase refer below example. 


    - **EX1**: `grid-template-columns: repeat (3, 200px)`
    repeat 3 times 重複3次 也就是欄設定為200px寬度。 

    - **EX2**: `grid-template-columns: repeat (6, 200px)` 
    `repeat 6 time with 200px each 重複6次 每欄為200px

    ![](https://i.imgur.com/DA2zo9D.png)


- #####  value as fraction  `fr `
we can also set to `fr` which is fraction value as below:
    - **EX**:  `grid-template-columns: 1fr 2fr 1fr` 
    We have 100%, the `first and third given 25%` of space, and `second one five 50%` of the space
    ![](https://i.imgur.com/Jha0Hdv.png)

- ##### value as `minmax`
We can also set `mimmax`, which you can provide `min` and `max width`. 
> `syntax`: `minmax(min, max);`

    - **EX**:  `grid-template-columns: repeat(3, minmax(200px, 1 fr));` 
    The column should be at least 200px, once less than 200px, column will start to overflow. 
    ![](https://i.imgur.com/nOwqXFq.png)


- #####  Compare `fr` and `px` different 比較FR 和PX 差別
    > `fr` 是以最大空間為大小， `PX` 是以實際`PIXEL` 為大小。請看圖更詳細看它們的差別
    > `Fraction` value take over all available space just like `%`
    > `Pixel` value will only set according to what you specify 

    ![](https://i.imgur.com/EP5bnQR.png)

--- 

#### grid-template-rows 列的高度 (row height- 列的高度)
Specifies the number of rows(height) in a grid layout. It\'s the same as the column except for instead set width, we set its height of it. The row also refers to X axis horizontal axis.

- ##### value as `PX` or `auto` 
> - 設定高度大小以`px`為單位，或 `auto`。
    > - 如果設用高度大小為`auto`就是內容，會把它展最大高度。請看我下面圖。We can also set other than px or auto, auto will stretch to max height
    > - 如果設定單一值(value)，就是第1列會設高度，其他列會用預設高度。If we set 1 parameter row hight only the first row will be set, the reest will use default height.

    - **Ex1**: (1 value 單一值) Set the first row to 100px
    `grid-template-rows: 100px;`
    - **Ex2**: (x value 自訂不同列的高度) set three row of different height
    `grid-template-rows: 100px 150px 200px;`
    - **Ex3**: (auto) set three row same height
    `grid-template-rows: auto auto auto;`

    ![](https://i.imgur.com/GEgbRRR.png)


- ##### value as `repeat` 
> - If we have three row of equal height
> - 如果有`同樣的大小`，我們可以用`repeat`這個函數，如下面例子。 we can also use the `repeat` option, to set all row with the same height, pelase refer below example. 

    - **EX1**: `grid-template-rows: repeat (3, 100px)`
    repeat 3 times 100px row height. 重複3次，也就是列設定為200px高度。
    - **EX2**: `grid-template-rows: repeat (2, 100px)`
    repeat 2 times 100px row height, the rest default. 重複2次，也就是列設定為100px高度。
    - **EX3**: `grid-template-rows: repeat (3, 100px) 200px`
    如果我們多加第4列，會出現一個新的列
    ![](https://i.imgur.com/11wcFuu.png)


- #####  compare value `fr ` vs `px` 
we can also set to `fr` which is fraction value or free space. In this example let assign `container height` to `400px`, `height: 400px`

 - **EX1**: `fr` value =>`grid-template-rows: repeat(3, 1fr);`
     We have set our height to be `400px`, and we also added a `fr` value in it, which will stretch available space to fill up the container. 
 - **EX2**: `px` value => `grid-template-rows: repeat(3, 100px);`
      We have set our height to be `400px`, and we also added a `px` value in it, which will sonly use the space you assign and left over with available space. 

    ![](https://i.imgur.com/PGsp0sY.png)

The biggest differenct between `fr` and `px` is `fr value` will take over all available free space, whereas `px value` won\'t. As you can see above picture, we have add `height` to the container, and apply `3 row with fr` will take all available space, and stretch. On the other side if you set the row with px, it will only apply the size and be left out with available space.

---

#### grid-template (shorthand)欄與列縮寫
shorthand for specifying rows and column. 這是上面我們所學的欄與列的縮寫。

> `Syntax`: `grid-template: ROW /COLUMN`

- **Ex:** ` grid-template: repeat(2, 1fr)/repeat(3, minmax(200px, 1fr));`

    ```
    .container{
        display: grid ; 
        border: 6px solid black;
    height: 400px;
    grid-template: repeat(3, 1fr) /repeat(3, minmax(200px, 1fr)); 
    }
    ```

![](https://i.imgur.com/9MGfSrA.png)

---

#### auto-fit and auto-fill value 

I wants to talk about this special value, which I didn\'t mention in above which is using auto-fit and auto-fill as a value. 


- `auto-fit`:
Auto-fit: we don\'t tell how many column you wants. See how ,much content is in each one and figure it out how many you can fit in it. 

- `auto-fill`:
FILLS the row with as many columns as it can fit. 

![](https://i.imgur.com/EdZ8iLr.png)

##### Examples

- **Example1 for auto-fit and auto-full**
```
.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: repeat(auto-fit, 150px);
    grid-gap: 10px;  
}

.item-9{
grid-column-end: -1;
}
```
![](https://i.imgur.com/fTT6CVy.png)

Resize browser, items will jump into next line when there is no much space left. 

- auto-fit: auto-fit will add one more column
- auto-fill: auto-fit will not.  

In above picture, as you can see if you wants to move item9 to the end, `auto-fit` will move to the `last new column`, but `auto-fill` will onlky stay on the `last column`. 

- **Example2 for `minmax() + auto-fill` for Responsive Grids**
> auto-fill+ minmax => autospace
> auto-fill FILLS the row with as many columns as it can fit.

```
.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    grid-gap: 10px; 
}
```
![](https://i.imgur.com/Z02NA5q.png)


- **Example3 for `minmax() + auto-fit` for Responsive Grids**
> auto-fit+ minmax => no autospace
> auto-fit FITS the CURRENTLY AVAILABLE columns into the space by expanding them so that they take up any available space. 

```
.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    grid-gap: 10px; 
}

```

![](https://i.imgur.com/z0uVd4T.png)

#### fit-content
It uses this forumular: min(maximum size, max(minimum size, argument)).  The fit-content() property use to defined function to put a limit on the maximum size of the division.

As you can see item-1 no matter how big I set the width, it will only use the width of it\'s content. 
![](https://i.imgur.com/nLpYhwi.png)

#### auto and fraction 
> I have mention both `fr` and `auto` in above, but when `fr` and `auto` use together, it will display differently. Both `auto` and `fr` minimum width of the content length, and use the avaiable space, if no space shrink it. 

- when `Auto` and `Fr` use together: 
Let me show you if `fr` and `auto` use together, `fr` win, they both flight for the remaining space, `auto` loses it/'s width and shrink down to min-with of content width. 
![](https://i.imgur.com/YB2JkDm.png)

> resource: https://www.rawkblog.com/2018/03/css-grid-understanding-grid-gap-and-fr-vs-auto-units/
---
#### grid-template-area
Let create code like below 

```
<div class="container"> 
        <div class="grid-item item-1">Item 1 </div>
        <div class="grid-item item-2">Item 2</div>
        <div class="grid-item item-3">Item 3</div>
        <div class="grid-item item-4">Item 4</div>
<style>

.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: 1fr 500px 1fr;
    grid-template-rows: 150px 150px 100px;
    grid-gap: 10px;  
    grid-template-areas: 
    "sidebar1 content sidebar2"
    "sidebar1 content sidebar2"
    "footer footer footer"    
}
```

![](https://i.imgur.com/6QBiH0N.png)

Let adjust the grid item like this:
``` 
.item-1{
  grid-area: sidebar1;
}
.item-2{
    grid-area: content;

}
.item-3{ 
    grid-area: sidebar2;
}
.item-4{ 
    grid-area: footer;
}
```
![](https://i.imgur.com/E9K9ZGe.png)

> Note: if you wants to leave empty use can use `.` like this: `footer footer .`

![](https://i.imgur.com/WHn0GhQ.png)

### 3. grid-auto-flow
- row: 排列方向以行為優先
- column: 排列方向以列為優先
- dense: 將網格項目非常緊密的排列在一起

#### Implicit and Explicit track 

In the previous properties we have learn grid-template, which you can refer it as explict track. In this section we will mention grid-aut0-flow, which you can refer it as implicit-track. So let dive into more detail between these two track in order to understand what's grid-auto-flow. Honestly this might not be use often, it depend. 

- Implicit: if you do not create it using
- Explicit: you create it either using grid-template-column or  grid-template-row properties

In the bottom the `first picture` you can see I ONLY `define the column`, the `row` will become `implicit` define by browser. The `second picture`  I `define the row`, so the `row` will become `explicit`. So there is no implicit. 
![](https://i.imgur.com/iRBkGjR.png)

So If I add `new grid items`, the `new created` items will become `implicit`. Orginal I have Items1~Items4, which i also declare 2 column, and 2 row. Now if I add `New items` (`item4 and item5`), it will become `implicit`, because we only `declare 2 column, and 2 row`, so the `two new extra item`, will become `implicit`. If we create another items 7-item8, it will also be `implicit`. 
![](https://i.imgur.com/NMd8EUw.png)

You can use the line to distinguish between is it `implict` or `explicit` track. In both picture above I have marked the arrow yo show you the line type.
![](https://i.imgur.com/SZjqzjC.png)

So we have an understaing of what\'s is `implicit and explicit track`, so let move to `grid-auto-flow` to see more example. 


#### grid-auto-flow:

- Control how auto placed items get inserted into the grid
> `grid-auto-flow` 属性通过控制自动布局算法的运作原理，精确指定自动布局的元素在网格中排列的方向。 **資料來源 - MDN**

> **syntax**: `grid-auto-flow: {row| column| dense| row dense| column dense}`
>> default the value is `row`

##### grid-auto-flow row and column
grid-auto-flow 設定，會依照設定的 `grid-template-columns` 數量去設定 column ，但假如是 row 的話
![](https://i.imgur.com/pVUQGId.png)

 So in below example we only define 2 column, but we have 3 grid item, the third items, will automatic flow to the next line or new row which is default, and it will become implict. So how do we lay next to the item2, so this is where we add grid-auto-flow. All the items in implict will lay in column rather than row(default)
![](https://i.imgur.com/Y1lv91s.png)

So if we create more grid-item, all the items will position it as colummn, next to each other. 

##### grid-auto-flow dense
dense is just like a space betwwen the track, so let me show you what's is dense. If we have a code like this: 
```
.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: 1fr 500px 1fr;
    grid-template-rows: 150px 150px 100px;
    grid-gap: 10px;  
}
```

Let add item with span on it. We will talk about `span` in below section. I just wants to show you what\'s dense.  In order to use `dense`, we need to have an empty spot or 
 
```
.grid-item:nth-child(4n){
background-color: yellow;
grid-column: 2 span;
}
```

>`.grid-item:nth-child(4n)` this mean every 4 item will use this styling

So As you can see below picture, item8 will overflow to new line, because there is no spot to store 2 span. 
![](https://i.imgur.com/xhFU8aB.png)

Now let add `grid-auto-flow` with `dense` and see what will happen.
    ```
    .container{
        display: grid ;  
        border: 5px black solid;  
        grid-template-columns: 1fr 500px 1fr;
        grid-template-rows: 150px 150px 100px;
        grid-gap: 10px;  
        grid-auto-flow: dense;
    }
    ```
In above I mention that `item8` have **no space and overflow** to next line. If we add `dense` properties, the **empty spot or track** will be replace by other items. Please refer below pciture for more detail.
![](https://i.imgur.com/WmP8XN9.png)

#### column and row (set width and height)
- `Grid-auto-column`: Setting default column width (same width)
    - **EX1**: `grid-auto-column: 100px`
    Value: pixel, %, minmax, auto(default)   
- `Grid-auto-row`: Setting default row height  (same height)
    - **EX2**: `grid-auto-row: 100px`
    Value: pixel, %, minmax, auto(default)
    ![](https://i.imgur.com/fyC05ha.png)
-  `Grid-auto-column` with different size
    - **EX3**: `grid-auto-column: 100px 500px 100px`
    ![](https://i.imgur.com/ZKOTjx5.png)


### 4. Gap 間距
> - Spacing between row and column  `<row gap> <column gap>`
> - specify the gap between columns using `column-gap`
> - specify the gap between rows using `row-gap`
> - value can be non negative value or a perentage 

#### Example gap 
- **EX1 column gap**: `column-gap: 20px`
欄之間的距 column's gap or Space between each other

- **EX2 row gap**: `row-gap: 20px;`
列之間的距 Row\'s gap or Space between each other

- **EX3 column and row gap**: `gap: 50px 20px;`
欄與列間距縮寫 shorthand for row-gap and column-gap
> **syntax** : `gap: row gap column gap`

![](https://i.imgur.com/iUZgkMc.png)


### 5. alignment and spacing within cell
- within grid cell:
    - justify-item for aligment => `row or X axis` 
    - alignment-item for aligment => `colummn or Y axis `
    - place-item: shorthand for `<align> ` `<justify>`

- within grid container:
    - justify-content=> `row or X axis` 
    - align-content => `colummn or Y axis `
    - place-content: shorthand for `<align> ` `<justify>`

![](https://i.imgur.com/TvTzvw3.png)


#### justify-items

- alignment along the `row or X axis 水平方向走(往右走)`
> syntax: `justify-items: {stretch| start| end | center}`
>> default the value is `stretch`

![](https://i.imgur.com/SxJoQTU.png)

```
.container{
display: grid ;
border: 4px solid black;
grid-template: repeat(3, 1fr)/repeat(3,minmax(200px, 1fr));
justify-items:end;
}
```

![](https://i.imgur.com/2roc6jX.png)

####  align-items

- alignment along the `column or Y axis 垂直方向走(往下走)`
> **syntax:** `align-items: {stretch| start| end| center}`
>> default the value is `stretch`

![](https://i.imgur.com/xq49IGU.png)

```
.container{
display: grid ;
height:400px;
border: 4px solid black;
grid-template: repeat(3, 1fr)/repeat(3,minmax(200px, 1fr));
justify-items: center;
align-items:center;
}
```

![](https://i.imgur.com/ajknAkc.png)


#### place-items 

- shorthand for align-items and justify-item
> **syntax**: `place-items : <align-items> <justify-item>`
There are two way we can set the value, with `2 value (start and end)`, or `1 value`, which both obtain the same value. 

- **EX1 place with two value**: `place-items: start end`
- **EX2 place with one value**: `place-items: center`


    ```
    .container{
    display: grid ;
    height:400px;
    border: 4px solid black;
    grid-template: repeat(3, 1fr)/repeat(3,minmax(200px, 1fr));
    place-items: start end
    }
    ```
    ![](https://i.imgur.com/MJnHIYA.png)


---
#### justify-content

- Alignment and spacing alone `row or X axis`
> syntax: `justify-content: { start |center | end |space-between| space-around |space-evenly }`
>> default the value is `start`

    ```
    .container{
    display: grid ;
    height: 800px;
    border: 6px solid black;
    grid-template: repeat(3, 200px)/ repeat(3, 200px);
    justify-content: start;
    }
    ```
The whole grid-item is a group, so when set `justify-content`,  `row`  will be move to `right or horizontal direction`. Please refer below picture for more detail.
![](https://i.imgur.com/Omn9ryA.png)


####  align-content

- Alignment and spacing alone `column or Y axis`
> syntax: `align-content: { start |center | end |space-between| space-around |space-evenly }`
>> default the value is `start`

The whole grid-item is a group, so when set `align-content`, `column` will move to `bottom or vertical direction`. Please refer below picture for more detail.

```
.container{
display: grid ;
height:800px;
border: 6px solid black;
grid-template: repeat(3,200px)/repeat(3,200px);
justify-content: space-around;
align-content: space-around;
}
```

![](https://i.imgur.com/I00vot2.png)

#### place-content 
- shorthand for align-content justify-content>
> **syntax**: `place-content : <align-content> <justify-content>`

- **EX1 place with two value**: `place-content: start end`
- **EX1 place with one value**: `place-content: center`
The whole grid-item is a group, so when set `place-content`, all the `row and column` will be move. Please refer below picture for more detail.
    ```
    .container{
    display: grid ;
    height:800px;
    border: 6px solid black;
    grid-template: repeat(3,200px)/repeat(3,200px);
    place-content: start end;
    }
    ```

![](https://i.imgur.com/rh1SXNT.png)


## Part 2-2 Grid Items (Child Properties)

Example code 
```
.container{
display: grid ;
border: 6px solid black;
grid-template: repeat(3, 200px)/repeat(3,200px);
}
```
![](https://i.imgur.com/IY9O8ZC.png)


### Items position
> Properties control the position of the item in the grid

> - Items position:
    - `column`:
        - Grid-column-start
        - Grid-column-end
    - `row`:
        - Grid-row-start
        - Grid-row-end
    - column and row（shorthand）:
        - Grid-column start end
        - Grid-row start end
> - `Value`: 
    - `line` => number　
     ![](https://i.imgur.com/8GdTUK2.png)
    - `span`: => span number
    ![](https://i.imgur.com/rcmyn3D.png)

Let use some example for more clear understand

#### example:

- Grid Line Example

```
.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: repeat(3, auto);
    grid-gap: 10px; 
}

.item-1{
grid-column-start: 2; 
grid-column-end: 3; 
}

.item-3{
grid-column: 1/-1; 
}
```
![](https://i.imgur.com/k1zUV7u.png)


- span example

> span start and end is auto: ` span 2`
> span start end with track　or line:`span 2/5`

```
.container{
    display: grid ;  
    border: 5px black solid;  
    grid-template-columns: repeat(4, auto);
    grid-gap: 10px; 
}

.item-1{
grid-column: 2 span;
grid-row:2 span;
}

.item-2{
grid-column: 2 span;
}

.item-4{
grid-column: 2 span/4;
}
```
![](https://i.imgur.com/bFa3CCp.png)



- Examples
 ![](https://i.imgur.com/JuvoJha.png)


### Alignment item (set single grid item)
- We can use alignment with `justify-items`, `align-items`, or `place-items` properties which apply to every item in container. 
- However If you wants to `alignment` for  `one single item`, you can use below with `self properties`.  
>   - `justify-self`: alignment along the `row axis`
>   - `align-self`: alignment along the `column axis`
>   - `place-self`: shorthand for `<align-self> <justify-self>`

#### justify-self
> syntax: `justify-self: {stretch |start |center|end}`
>> default the value is `stretch`

```
.container{
    display: grid ;
    border: 6px solid black;
    grid-template: repeat(3, 200px)/repeat(3,200px);
}

.grid-item{
color: #000;
font-size: 1.5rem;
padding: 1rem;
text-align: center;
}
.item-1{
    background-color: red;
    grid-column: 1/span 2;
    grid-row: 1/span 2;

}
.item-2{
    background-color: yellow;
   justify-content: stretch;
}
```
![](https://i.imgur.com/RTxjQHM.png)



#### align-self

> syntax:  `align-self: {stretch |start |center|end}`
>> default the value is `stretch`

```
.item-1{
    background-color: red;
    grid-column: 1 /span 2;
    grid-row: 1/span 2;

}
.item-2{
    background-color: yellow;
    justify-self: center;
   align-self: stretch;
}
```

![](https://i.imgur.com/VdDJcfP.png)

#### place-self

- Shorthand for align-self and justify-self
> syntax:  `place-self : <align-self> <justify-self>`

```
.item-1{
    background-color: red;
    grid-column: 1 /span 2;
    grid-row: 1/span 2;

}
.item-2{
    background-color: yellow;
place-items: start end;
}
```

![](https://i.imgur.com/12SyaX5.png)


---

## Part 3 Example and Layout
### EXample 1 Layout
#### html 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style2.css">
</head>
<body>
    <div class="grid-container" >       
        <header class="grid-item">Header</header>
        <main class="grid-item">Main</main>
        <aside class="grid-item">Aside</aside>
        <section class="grid-item">section</section>
        <footer class="grid-item">footer</footer>
    </div>
</body>
</html>
```
#### output
![](https://i.imgur.com/rvmlTEj.png)

#### EXample 1-1 Layout without gridArea

```
*{
    margin: 0px;
    padding: 0px;
}

body{
    background-color: lightgray;
    text-align: center;   
}
body .grid-item{
    border-radius: 40px;
    font-size: 5rem;
    background-color: blue;
    }

.grid-container{
    width: 90%;
    margin: auto;
    display: grid ;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 200px 400px 400px 200px;
    grid-gap: 20px;;
} 

header{
grid-column: 1/5;
grid-area: h;
}
main{
    grid-column: 1/4;
    grid-row: 2/4;
}

aside{
}

section{
}

footer{
    grid-column: 1 /5;
}
```
#### EXample 1-2 Layout with gridArea
以grid area 方式來切版，跟上面範例一樣。Same as above just change to grid area。0px

- CSS
```
*{
    margin: 0px;
    padding: 0px;
}
body{
    background-color: lightgray;
    text-align: center;  
}
body .grid-item{
    border-radius: 40px;
    font-size: 5rem;
    background-color: blue;
    }

.grid-container{
    width: 90%;
    margin: auto;
    display: grid ;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 200px 400px 400px 200px;
    grid-gap: 20px;;

    grid-template-areas: 
    'h h h h'
    'm m m a'
    'm m m s'
    'f f f f'   
    ;
} 
header{
/* grid-column: 1/5; */
grid-area: h;
}
main{
    /* grid-column: 1/4;
    grid-row: 2/4; */
    grid-area: m;
}
aside{
    grid-area: s;
}
section{
    grid-area: a;
}
footer{
    /* grid-column: 1 /5; */
    grid-area: f;
}
```
#### Compare with and without grid are

![](https://i.imgur.com/rvmlTEj.png)

### EXample 2 Layout
#### HTML:

```
<body>
  <h1> GRID </h1>
  <div class="container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
  <div>7</div>
  <div>8</div>
  <div>9</div>
  </div>
</body>
```

#### CSS:

```
.container {
  background-color: blue;
  padding: 10px;
  color: black;
  /* 格線排版   */
  display: grid;
  /*  columns  */
  grid-template-columns: auto auto auto;
  /*  row height  */
   grid-template-rows: 80px  200px 50px;
   /*  gap  */
   grid-gap: 40px 60px;  
}

.container > div{
   background-color: yellow;
  padding: 20px 0;
  font-size: 30px;
  text-align: center;  
}

```
#### output 
![](/images/gridexample.png)

## Reference
https://www.quackit.com/css/grid/tutorial/explicit_vs_implicit_grid.cfm
https://pjchender.dev/css/css-grid-layout/
https://css-tricks.com/snippets/css/complete-guide-grid/
https://shunnien.github.io/2018/03/18/css-grid-06/
https://www.geeksforgeeks.org/css-fit-content-property/
https://www.rawkblog.com/2018/03/css-grid-understanding-grid-gap-and-fr-vs-auto-units/
