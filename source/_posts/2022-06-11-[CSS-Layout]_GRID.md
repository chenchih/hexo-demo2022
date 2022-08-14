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

- display (enable grid propertis 啟動GRID)
- Grid Container(parent Properties)
	- grid-template
	  - grid-template-column 
	  - grid-template-row 
	  - grid-template
	  - grid-template-areas (進行中)	  
	- gap 
	  - column-gap
	  - row-gap
	  - gap
	- Alignment & Spacing
		- within grid cell
			- justify-items
			- align-items
			- place-items 
		- within grid container
			- justify-content
			- align-content
			- place-content
	- grid-auto-flow
	  - grid-auto-column
	  - grid-auto-rows
	  - grid-auto-flow 
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
> - `Grid line`: Grid的線條之間。Horizontal or Vertical divided line in a grid
> - `Grid Cell`: intersection of the grid. grid 的最小單位
> - `Grid-Area`: 
> - `Grid-Track(格線軌道)` 
    - `explicit-track`: 透過 `grid-template-columns` 與 `grid-template-rows`屬性定義了行與列
    - `implicit track`: 透過 `grid-auto-rows` 和 `grid-auto-columns` 來定義。

![](https://www.quackit.com/pix/stock/css_grid_explicit_and_implicit_track_sizing.png)

![terms](https://i.imgur.com/eYFvrl5.png)

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
以下我開使介紹Container 和 Items相properties。

### 1. display
By `default` the content has created single column grid for the items. All of the grid items lay in `row`, which behave like `block element`, so this is why even if you don't add `display: grid` the content will lay block. If you  `don't` wants grid container to `display in block`, you can change it to `inline-block`. There are two properties for display as below:  

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
 > - `grid-template-column` set how many column 設定幾個欄
 > - `grid-template` shortcut for row and column 列與欄的縮寫

> 他有很多不同方式來設他的值(value)如下面方法:
>>- non-negative length value like 任何正數 `px`, `%` , `rem`等等
>>- `auto`: determined by the size of the container, and on the size of the content of the items。尺寸是以照內容的寬度呈現
>>- `fr`: 就是fraction ，指的是 container扣掉 grid-gap `後的空間加以分配`，用法類似 `flex-grow` 和 `flex-shrink`。 Fraction will take free space avaiable of the container anf gap space , which is related to `flex-grow` 和 `flex-shrink` 
>>- `repeat()`可重複某值 and `minmax()`可將值限定在某區間，傳入兩個參數，最小值與最大值

#### grid-template-columns 欄的寬度
住要是做來設定幾個欄位。Specifies number of columns in a grid layout, each value represent the size of column. 
> Symtax: grid-template-columns: X-column` 
>> `1 column`:　grid-template-columns: 100px;
>> `3 column`:　grid-template-columns: 100px 100px 300px;

![](https://i.imgur.com/bgApvOe.png)

- ##### value as `PX` or `auto` 
> - 設定寬度大小以`px`為單位，或 `auto`。
    > - 如果設用寬度大小為`auto`就是內容，會把它展最大寬度。請看我下面圖。We can also set other than px or auto, auto will stretch to max width
    > - 如果設定單一值(value)，就是1欄，以我的圖設3個px 說明3欄。Value can set with 1 paramter size(for one colulmn), set 3 paramter size (for 3 column)
 
- EX1(自訂不同欄的寬度):
`grid-template-columns:100px 200px 300px` 
- Ex2: 我們也可以用`auto` 自動調寬度大小，如下面:
`grid-template-columns: auto auto auto;`
![](https://i.imgur.com/8txVTrW.png)


It will create three column, `first column is 100px`, `second is 200px`, and `third is 300px`. Since we define three column, so the forth items will be in second row. 

- #### value as `repeat` 
> - 如果有`同樣的大小`，我們可以用`repeat`這個函數，如下面例子。 We can also use the `repeat` option, to set all column with the same width, pelase refer below example. 

> - EX1: `grid-template-columns: repeat (3, 200px)`
repeat 3 times 重複3次 也就是欄設定為200px寬度。

> - EX2: `grid-template-columns: repeat (6, 200px)` 
repeat 6 time with 200 px each 重複6次 每欄為200px

![](https://i.imgur.com/DA2zo9D.png)


- ####  value as fraction  `fr `
we can also set to `fr` which is fraction value as below:

> - `grid-template-columns: 1fr 2fr 1fr` 

We have 100%, the `first and third given 25%` of space, and `second one five 50%` of the space

![](https://i.imgur.com/Jha0Hdv.png)

- #### value as `minmax`
We can also set `mimmax`, which you can provide `min` and `max width`. 
> syntax: `minmax(min, max);`
>> `grid-template-columns: repeat(3, minmax(200px, 1 fr));` 
The column should be at least 200px, once less than 200px, column will start to overflow. 

![](https://i.imgur.com/nOwqXFq.png)


####  Compare `fr` and `px` different 比較FR 和PX 差別
> `fr` 是以最大空間為大小， `PX` 是以實際`PIXEL` 為大小。請看圖更詳細看它們的差別
> `Fraction` value take over all available space just like `%`
> `Pixel` value will only set according to what you specify 

![](https://i.imgur.com/EP5bnQR.png)

--- 

### grid-template-rows 列的高度
Specifies the number of rows(height) in a grid layout
It\'s same as columnm expect instead set width, we set the height of it

- #### value as `PX` or `auto` 
> - 設定高度大小以`px`為單位，或 `auto`。
    > - 如果設用高度大小為`auto`就是內容，會把它展最大高度。請看我下面圖。We can also set other than px or auto, auto will stretch to max height
    > - 如果設定單一值(value)，就是第1列會設高度，其他列會用預設高度。If we set 1 parameter row hight only the first row will be set, the reest will use default height.

- Ex1: (1 value 單一值) Set the first row to 100px
`grid-template-rows: 100px;`
- Ex2: (x value 自訂不同列的高度) set three row of different height
`grid-template-rows: 100px 150px 200px;`
- Ex3: (auto) set three row same height
`grid-template-rows: auto auto auto;`

![](https://i.imgur.com/GEgbRRR.png)


- ### value as `repeat` 
> - If we have three row of equal height
> - 如果有`同樣的大小`，我們可以用`repeat`這個函數，如下面例子。 we can also use the `repeat` option, to set all row with the same height, pelase refer below example. 

> - EX1: `grid-template-rows: repeat (3, 100px)`
repeat 3 times 100px row height. 重複3次，也就是列設定為200px高度。

> - EX2: `grid-template-rows: repeat (2, 100px)`
repeat 2 times 100px row height, the rest default. 重複2次，也就是列設定為100px高度。

>  - EX3: `grid-template-rows: repeat (3, 100px) 200px`

如果我們多加第4列，會出現一個新的列

![](https://i.imgur.com/11wcFuu.png)


- ###  compare value `fr ` vs `px`  比較FR 和PX 差別
we can also set to `fr` which is fraction value as below:

> set container height:400px: `height: 400px`
> `grid-template-rows: repeat(3, 1fr);`
We have set our height to be `400px`, and we also added a `1fr` value in it, which will stretch avaible space to fill up the container. 
![](https://i.imgur.com/PGsp0sY.png)

---

### grid-template (shorthand)欄與列縮寫
shorthand for specifying rows and column. 這是上面我們所學的欄與列的縮寫。

> Symtax: `grid-template: ROW /COLUMN`
>> Ex: ` grid-template: repeat(2, 1fr)/repeat(3, minmax(200px, 1fr));`

#### Example 
```
.container{
    display: grid ; 
    border: 6px solid black;
   height: 400px;
   grid-template: repeat(3, 1fr) /repeat(3, minmax(200px, 1fr)); 
}
```

![](https://i.imgur.com/9MGfSrA.png)



### 3. Gap 間距
> - Spacing betwwen row and column  `<row gap> <column gap>`
> - specify the gap between columns using `column-gap`
> - specify the gap between columns using `row-gap`
> - value can be non negative value or a perentage 

#### Example gap 
- 欄之間的距 `column's gap or Space` between each other
> ex: `column-gap: column-gap: 20px;`

- 列之間的距 `Row's gap or Space` between each other
> ex: `column-gap: column-gap: 20px;`

- 欄與列間距縮寫 `shorthand for row-gap and column-gap`
> syntax: gap: row gap column gap
>> ex: `gap: 50px 20px; `

![](https://i.imgur.com/cyDRkxM.png)


### 4. aligment and spacing within cell
- within grid cell:
    - justify-item for aligment => row axis
    - alignment-item for aligment => colummn axis
    - place-item: shorthand for `<align> ` `<justify>`

- within grid container:
    - justify-content=> row axis
    - align-content => column axis
    - place-content: shorthand for `<align> ` `<justify>`

![](https://i.imgur.com/upKxT1s.png)


#### justify-items

- alignment along the row axis 
> syntax: `justify-items: {stretch| start| end | center}`
>> default the value is `stretch`

![](https://i.imgur.com/IW1UZcX.png)

####  align-items

- alignment along the column axis 
> syntax: `align-items: {stretch| start| end| center}`
>> default the value is `stretch`

![](https://i.imgur.com/AUn3KYS.png)


#### place-items 

- shorthand for align-items justify-item>
> syntax: `place-items : <align-items> <justify-item>`
>> example1: `place-items: start end` 
>> example2: `place-items: center` 

![](https://i.imgur.com/n1mH6JS.png)


---
#### justify-content

- Alignment and spacing alone `row axis`
> syntax: `justify-content: { start |center | end |space-between| space-around |space-evenly }`
>> default the value is `start`

##### Example: 

```
.container{
display: grid ;
height: 800px;
border: 6px solid black;
grid-template: repeat(3, 200px)/ repeat(3, 200px);
justify-content: start;
}
```

The whole grid-item is a group, so when set `justify-content`,  `row`  will be move  by horizontal direction. Please refer below picture for more detail.

![](https://i.imgur.com/Omn9ryA.png)


####  align-content

- Alignment and spacing alone `column axis`
> syntax: `align-content: { start |center | end |space-between| space-around |space-evenly }`
>> default the value is `start`

The whole grid-item is a group, so when set `align-content`, `column` will move by vertical direction. Please refer below picture for more detail.

![](https://i.imgur.com/I00vot2.png)

#### place-content 
- shorthand for align-content justify-content>
> syntax: `place-content : <align-content> <justify-content>`
>> example1: `place-content: start end` 
>> example2: `place-content: center`

The whole grid-item is a group, so when set `place-content`, all the `row and column` will be move. Please refer below picture for more detail.

![](https://i.imgur.com/rh1SXNT.png)

### 5. grid-auto-flow
- row: 排列方向以行為優先
- column: 排列方向以列為優先
- dense: 將網格項目非常緊密的排列在一起

#### grid-auto-flow:

- Control how auto placed items get inserted into the grid
> grid-auto-flow 属性通过控制自动布局算法的运作原理，精确指定自动布局的元素在网格中排列的方向。
資料來源 - MDN

grid-auto-flow 設定，會依照設定的 grid-template-columns 數量去設定 column ，但假如是 row 的話

> syntax: `grid-auto-flow: {row| column| dense| row dense| column dense}`
>> default the value is `row`

![](https://i.imgur.com/pVUQGId.png)

#### column and row
- Grid-auto-column: Setting default column width
    > EX: `grid-auto-column: 100px`
    >> Value: pixel, %, minmax, auto(default)

- Grid-auto-row: Setting default column height
    > EX: `grid-auto-row: 100px`
    >> Value: pixel, %, minmax, auto(default)

![](https://i.imgur.com/fyC05ha.png)



## Part 2-2 Grid Items (Child Properties)
Example code 
```
.container{
display: grid ;
border: 6px solid black;
grid-template: repeat(3, 200px)/repeat(3,200px);
}
```
![https://i.imgur.com/IY9O8ZC.png]


### Items position
> - Properties control the position of the item in the grid

> - Items position:
    - column:
        - Grid-column-start
        - Grid-column-end
    - row
        - Grid-row-start
        - Grid-row-end
    - clumn and row:
        - Grid-column (shorthand)
        - Grid-row (shorthand)
> - Value: 
    - grid line number　
    - Number of column or row item has to span
    ![](https://i.imgur.com/8GdTUK2.png)

#### example: 

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

![](https://i.imgur.com/RTxjQHM.png)

#### align-self

> syntax:  `align-self: {stretch |start |center|end}`
>> default the value is `stretch`

![](https://i.imgur.com/VdDJcfP.png)

#### place-self

- Shorthand for align-self and justify-self
> syntax:  `place-self : <align-self>< justify-self> `

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
![](https://i.imgur.com/mbIxcXc.png)

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