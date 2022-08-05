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
- 現在我們在做網頁排版，最流行都是用 `GRID` and `Flex`。 我是剛學排版，以前都用`position`
- GRID 主要是 可以控制欄和列。

## 參數：
- `grid-template-columns: auto auto auto;`
  - 3個 `auto` 就是3 rows
```css=
   grid-template-columns: auto auto auto;
```
- `grid-template-rows: `
  - row 高度
```grid-template-rows: 80px  200px 50px;```
- `grid-gap`
  -  間距
```
grid-gap: 40px 60px
```

## Example:
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
## output 
![](/images/gridexample.png)


## Grid Example:
我要介紹Flex Example

- display
- grid-tempalte
  - grid-template-column 
  - grid-tempalte-row 
  - grid-tempalte
- gap 
  - column-gap
  - row-gap
  - gap
- justify-items
- align-items
- place-items 
- justify-content
- align-content
- place-content
- grid-auto
  - grid-auto-column
  - grid-auto-rows
  - grid-autp-flow 
### HTML
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
### CSS
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
### 1. Display 
By default all the content are lay column, which lay like  block element. 
> `display: grid` lay block level

If you don't want block element then change it to 
> `display: inline-grid` lay inline level 

- code: 
```
.container{
display: grid ; 
border: 6px solid black;
}
```

## 2. grid-template
we can use `grid-template-row` or `grid-template-column`
value can be:
- non-negative length value like `px`, `%`
- `fraction` of the free space avaiable
- `repat()` and `minmax()`

### grid-template-columns
specifies number of columns in a grid layout, each value represent the size of column. so let set it as below:
> `grid-template-columns:100px 200px 300px`

It will create three column, first column is 100px, second is 200px, and third is 300px.

since we define three column, so the forth items will be in second row. 

#### value as repeat 
we can also use the `repeat` option, when all column have same width like this:
> `grid-template-columns: repeat (3, 200px)` //repeat 3 times 
> `grid-template-columns: repeat (6, 200px)` //repeat 6 time with 200 px each
#### value as fraction  `fr `
we can also set to `fr` which is fraction value as below:
> `grid-template-columns: 1fr 2fr 1fr` 
This mean: first and third given 25% of space, and second one five 50% of the space

#### value as minmax 
> `grid-template-columns: repeat(3, minmax(200px, 1 fr));` 
we can use minmax 
The column should be at least 200px, once less than 200px, column will start to overflow. 


### grid-template-row
- specifies the number of rows(height) in a grid layout
It's same as columnm expect instead set width, we set the height of it

Set the first row to 100px
> grid-template-rows: `100px;`

set three row of differenrt height
> `grid-template-rows: 100px 150px 200px;`

using repeat, we have three row of equal height
> `grid-template-rows: repeat(3, 100px);`

> `height: 400px`
> `grid-template-rows: repeat(3, 1f);`
>> three row column grow to take avaiable space


```
.container{
    display: grid ; 
    border: 6px solid black;
    grid-template-columns: repeat(3, minmax(200px, 1fr));
    grid-template-rows: 100px;
}
```
### grid-template (shorthand)
- shorthand for specifying rows and coluknb
> syntax: `grid-template: ROW /COLUMN`
>> ` grid-template: repeat(2, 1fr)/repeat(3, minmax(200px, 1fr));`


.container{
    display: grid ; 
    border: 6px solid black;
   height: 400px;
   grid-template: repeat(3, 1fr) /repeat(3, minmax(200px, 1fr)); 
}


## 3. gap properties: spacing betwwen row and column
specify the gap between columns using column-gap
specify the gap between columns using row-gap
specify both row and column using gap: `<row gap> <column gap>`
value can be non negative value or a perentage 


- column:
> example: `column-gap: 20px;`

- row:
> example: `column-gap: 20px;`

- gap: (shorthand for row and column gap)
> syntax: gap: row gap coluknb gap
>> example: `gap: 40px 20px; `

## 4. aligment and spacing within cell
- justify item for aligment => row
- alignment item for aligment => colummn axis
- place item: shorthand for `<align> ` `<justify>`

### justify-items
- default the value is `stretch`
- valu: {stretch, start, end, center}
###  align-items
- default the value is `stretch`
- value: {stretch, start, end, center}


### place-items
> shorthand : `<align-items>` `<justify-item>`
>> example1: place-items: start end

## 
### justify-content
### align-content
### place-content