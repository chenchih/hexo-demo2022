---
title: CSS LAYOUT - GRID 介紹
date: 2022-06-11 09:52:52
tags:
- 前端文
- CSS
categories:
- WEB
- [WEB, CSS]

---
# CSS Example: GRID
- 現在我們在做網頁排版，最流行都是用 `GRID` and `Flex`。 我是剛學排版，以前都用`position`
- GRID 主要是 可以控制欄和列。

## 參數：
- `grid-template-columns: auto auto auto;`
  - 3個 `auto`就是3 rows

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
  <h1> GRID  </h1>
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
