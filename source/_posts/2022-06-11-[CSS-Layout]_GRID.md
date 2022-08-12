---
title: CSS LAYOUT - GRID 介紹
date: 2022-06-11 09:52:52
tags:
- Frontend
- CSS
categories:
- [WebDev, CSS]

---
# CSS Example: GRID
- 現在我們在做網頁排版，最流行都是用 `GRID` and `Flex`。想要分享相關Grid 相關設定和用法，在早期都用以前都用`position`
用`position`或`float`等等排版。
- GRID 可以用用二維排版(row and colulmn)，反之`Flex`只能選用一維(row or colulmn)。
---
> 以下是所有<font color="red">`GRID` Properties </font>，我整理好分類，這樣才好董或記。如果有學會或用過`GRID`，這會更好理解。

- display (enable grid propertis 啟動GRID)
- grid Container(parent父)
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
	  - grid-autp-flow 
- Grid item(Child 子)
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
	
## GRID 架構 Structure & Terminology
### Container 和 Items 差別：
> `Grid Container`: 盒子的最外層Parent 
> `Grid items`: 盒內層Children 
> 其實跟Flex一樣，都需要有container and items

![container and items of GRID](https://i.imgur.com/g882pUK.png)

### 了解相關GRID terms
> `Grid line`: grid的線條之前 horizontal or vertical dived line in a grid
> `Grid Cell`: intersection of the grid
> `Grid-Track`:
> `Grid-Area`: 

![terms](https://i.imgur.com/eYFvrl5.png)


## Grid Container
- 以下會用到的HTML and CSS程式碼。Example Code for demo on different properties
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
/* display: grid ; */
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

### 1. display
By default all the content are lay column, which lay like  block element. 
>  Display properties : `<grid>` or `<inline-grid>`
>> `display: grid` : default by row and stretch behave to block element 
>> `dispplay: inline-grid`: will not display in block element 

#### Display example:
```
.container{
display: grid ; //or inline-grid
border: 6px solid black;
}
```

![](https://i.imgur.com/3golNqE.png)

## 2. grid-template 
we can use `grid-template-row` or `grid-template-column`

> 直為以下方式value can be:
- non-negative length value like `px`, `%`
- `fraction` of the free space avaiable
- `repeat()` and `minmax()`

### grid-template-columns 欄的寬度
設定欄為。Specifies number of columns in a grid layout, each value represent the size of column. so let set it as below:
>EX1: `grid-template-columns:100px 200px 300px` 
我們也可以這樣設`auto` 不需要設定大小，如下面:
> Ex2: `grid-template-columns: auto auto auto;`

It will create three column, first column is 100px, second is 200px, and third is 300px. Since we define three column, so the forth items will be in second row. 

#### value as `repeat` 
如果有同樣的大小，我們可以用`repeat`這個函數，如下面例子。
we can also use the `repeat` option, when all column have same width like this:
> `grid-template-columns: repeat (3, 200px)` 
>> //repeat 3 times 重複3次 也就是欄設定為200px寬度。

> `grid-template-columns: repeat (6, 200px)` 
>> //repeat 6 time with 200 px each

#### value as fraction  `fr `
we can also set to `fr` which is fraction value as below:
> `grid-template-columns: 1fr 2fr 1fr` 
This mean: first and third given 25% of space, and second one five 50% of the space

#### value as `minmax`
We can also set mimmax, which you can provide min and max width. 
> syntax: minmax(min, max);
>> ex: `grid-template-columns: repeat(3, minmax(200px, 1 fr));` 
The column should be at least 200px, once less than 200px, column will start to overflow. 

### grid-template-rows 列的高度
- Specifies the number of rows(height) in a grid layout
- It's same as columnm expect instead set width, we set the height of it

> Set the first row to 100px
>> `grid-template-rows: 100px;`

> set three row of different height
>> `grid-template-rows: 100px 150px 200px;`

> 也可以這樣設
>> `grid-template-rows:auto auto auto;`

#### value as `repeat` 
If we have three row of equal height

> `grid-template-rows: repeat(3, 100px);`

> `height: 400px`
> `grid-template-rows: repeat(3, 1f);`
>> three row column grow to take avaiable space

#### Example 
```
.container{
    display: grid ; 
    border: 6px solid black;
    grid-template-columns: repeat(3, minmax(200px, 1fr));
    grid-template-rows: 100px;
}
```

### grid-template (shorthand)
- shorthand for specifying rows and column
> syntax: `grid-template: ROW /COLUMN`
>> ` grid-template: repeat(2, 1fr)/repeat(3, minmax(200px, 1fr));`

#### Example 
.container{
    display: grid ; 
    border: 6px solid black;
   height: 400px;
   grid-template: repeat(3, 1fr) /repeat(3, minmax(200px, 1fr)); 
}


## 3. Gap 間距
> Spacing betwwen row and column  `<row gap> <column gap>`
> specify the gap between columns using `column-gap`
> specify the gap between columns using `row-gap`
> value can be non negative value or a perentage 

### Example
```
grid-gap: 40px 60px
```
specify both row and column using gap:

### column-gap:
> example: `column-gap: 20px;`

### row-gap:
> example: `column-gap: 20px;`

### gap: (shorthand for row and column gap)
> syntax: gap: row gap column gap
>> example: `gap: 40px 20px; `

## 4. aligment and spacing within cell
- justify item for aligment => row
- alignment item for aligment => colummn axis
- place item: shorthand for `<align> ` `<justify>`

### justify-items
- default the value is `stretch`
- value: {stretch, start, end, center}

###  align-items
- default the value is `stretch`
- value: {stretch, start, end, center}

### place-items
> shorthand : `<align-items>` `<justify-item>`
>> example1: place-items: start end


### justify-content

### align-content
### place-content





## Example and Layout
### EXample 1 Layout
### EXample 2 Layout

### EXample 3 Layout
- HTML: 我宣告一個parent，裡麵包div

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

- CSS:

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