---
title: Emmet 指令and VSCode
date: 2022-06-24 20:23:24
tags: 
- Emmet
- vscode
categories:
- devtool

---

# Emmet
我想分享一些最常用到的`Emmet`和`VScode`相關指令。如果會`Emmet`我們可以提高我們在編寫`HTML`的時間。我們不需要打麼長的與法。

## 1. html初始结構
> 指令:`！` =>tab or enter
```html=
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
</body>
</html>
```
## 2. CSS連結
> 指令: `link:css` =>tab or enter
在<head>裡面加
```html
<link rel="stylesheet" href="style.css">
```

## 3.隱式TAG , id（#）,class（.）
- ###  div tag:`.name`
    > 指令: `.test`
```html
<div class="test"></div>
```

- ### list tag: 
    >指令: `ul>.test$*3`
```html=
<ul>
    <li class="test1"></li>
    <li class="test2"></li>
    <li class="test3"></li>
</ul>
```
- ### id指令：`#`
    > **Ｓyntax:**`div.idname`
    >> 指令:`div#test`

    ```html
    <div id="test"></div>
    ```
- ### class指令`.`
    > **Ｓyntax:** `div.classname`
    >> 指令:`div.test`

    ```html
    <div class="test"></div>
    ```

- ### em 和 span :
    >**Ｓyntax:**`tag>.class`
    >>指令:`em>.class`
```html
<em><span class></span></em>
```
- ### 表格 table
> 指令:`table>.row>.col` 
```html=
<table>
    <tr class="row">
        <td class="col"></td>
    </tr>
</table>
```
- ### option  
> **Ｓyntax:** `select>classname`
>> 指令:`select>.test$*5` 
```html=
<select name="" id="">
    <option class="test1"></option>
    <option class="test2"></option>
    <option class="test3"></option>
    <option class="test4"></option>
    <option class="test5"></option>
</select>
```

## 4.属性 attribute`$`，`@`
- ### `$`代表一位数，后面更上`*`數字就代表從1遞增到寫得位置。
#### **Example $**
> `ul>li.test$*3`
```html=
<ul>
    <li class="test1"></li>
    <li class="test2"></li>
    <li class="test3"></li>
</ul>
```
- ### `@`自定從N開始遞增可以用：`$@+數字*數字`
#### **Example `$`**
> `ul>li.test$*3{測試$} `
```html=
<ul>
<li class="test1">測試1</li>
<li class="test2">測試2</li>
<li class="test3">測試3</li>
</ul>
```
## 6. 重復指令:`*`自動生成重複標籤
> **Ｓyntax:** `tag * N` #N重複N數
####  **Example1**
>指令: `div*3`
```html=
<div></div>
<div></div>
<div></div>
```
#### **Example2** 
> 指令:`ul>li*3`
```html=
<ul>
<li></li>
<li></li>
<li></li>
</ul>
```

## 7. 文本Text和自動計數文本（{}）
### 7.1 基本文本
#### **Example基本文本**
> **Ｓyntax:** `div{這是一段文本}`
>> 指令: `div{hello}`
```html=
<div>hello</div>
```
### 7.2 自動計數文本
生成重複項時增加一個序號，只需要加上$符號即可
#### **Example1 文本加$**
> 指令: `div*3{test$}`
```html=
<div>test1</div>
<div>test2</div>
<div>test3</div>
```
#### **Example2 里面填寫内容，可以和`$`一起组合使用}）**
>  指令: `ul>li.test$*3{test$}`
```html=
<ul>
    <li class="test1">test1</li>
    <li class="test2">test2</li>
    <li class="test3">test3</li>
</ul>
```
#### **Example3** 
> 指令:`ul>li.item$@-*3`
```html=
<ul>
    <li class="item3"></li>
    <li class="item2"></li>
    <li class="item1"></li>
</ul>    
```
#### **Example4 自動計數(numbering)** 
> 指令:`ul>li.item\${item number:\$}*3`
```html=  
<ul>
    <li class="item1">item number:1</li>
    <li class="item2">item number:2</li>
    <li class="item3">item number:3</li>
</ul>
``` 
## 8. Nesting operators 子:`>`,兄:`+`,父`^`
縮寫元素放置在生成的樹中，是否應放置在上下文元素的內部或附近
> - 子節點指令`>`
> - 同級節點指令`+`
> - 父級節點指令：`^`

- ### 8.1 子節點指令`>`(Example:`div>ul>li>p`)
通過`>`標識元素可以生成嵌套子級元素，可以配合元素屬性進行連寫

#### **Example1**
> 指令: `div>ul>li>p`
```html=  
<div>
    <ul>
        <li>
            <p></p>
        </li>
    </ul>
</div>
``` 
#### **Example2**
> 指令: `div#pageId>ul>li`
```html=  
<div id="pageId">
<ul>
<li></li>
</ul>
</div
``` 
- ### 8.2 兄弟/同級節點指令`+` 
通過`+`標識元素字元表示生成兄弟/同級級元素

#### **Example1**
> 指令: `div+ul+p`
```html=  
<div></div>
<ul></ul>
<p></p>
```

#### **Example2:** 
> 指令:`div#pageId+div.child`
```html=
<div id="pageId"></div>
<div class="child"></div>
```

#### **Example3:完整架構**
>指令:`.top+.banner+.box+.footer`
```html=
<div class="top"> </div>
<div class="banner"></div>
<div class="box"></div>
<div class="footer"></div>  
``` 
- ### 8.3 父級/上级節點指令`^` 
通過`^`標識元素，用於生成父級元素的同級元素，從這個字元所在位置開始，搜尋左側最近的元素的父級元素並生成其兄弟級元素.

#### **Example1**
> 指令: `div>ul>li^div`
(li的上级，與ul成了兄弟關系,所以兩個就是上上级）
```html=
    <div>
        <ul>
            <li></li>
        </ul>
        <div></div>
    </div>
``` 
#### **Example1**
> 指令: `div>ul>li^div`
```html=
    <div>
        <ul>
            <li></li>
        </ul>
        <div></div>
    </div>
```
#### **Example2**
> 指令:`div>p.parent>span.child^ul.brother>li`
```html=
<div>
<p class="parent"><span class="child"></span></p>
    <ul class="brother">
        <li></li>
    </ul>
</div>
```

## 9. 分组Grouping()
#### **Example1**
> 指令:`div>(ul>li>a)+div>p`
>>如果不加括號的话，`a+div`這樣`div`就是和`a`是兄弟關系了，會包含在`li`里面。
```html=
    <div>
        <ul>
            <li><a href=""></a></li>
        </ul>
        <div>
            <p></p>
        </div>
    </div>
```
#### **Example2**
>指令: `div>(ul>li+span)>a`
```html=
<div>
    <ul>
        <li></li>
        <span></span>
    </ul>
    <a href=""></a>
</div>
```
# vscode shortcut
TBD

