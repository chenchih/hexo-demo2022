---
title: JS Basic Code 基本
date: 2022-07-30 07:59:48
tags: JS
categories:
- [WebDev, CSS]
---

## 基本

### How to run JS
- Browser- inspect 
    - Method1: 
    > Go to inspect > console

    - Method 2: 
    > inspect> sources> snipperts> create js file
    
- NodeJS environment
    > 寫 `.js` file 
    > node XXX.js

### adding comment 
`//` ignore js comment

### 顯示 print
- `console.log()` 顯示在console
- `alert()` 跳出顯示
- `document.write("\<h1>hello <br\/>")`

## JS　語法 
### １. declare variable 宣告變數
- `let` (新)可以取代var
> ex: 
>> `let myName= "chenchih"`
>> `console.log(myName)`
- `var`
- `const` 
> must be inital and not able to change 
> 不被修改變數。如果不想被人修改
```
const test= "heloo"
test="world"
console.log(test) //error
```

### 2. Data Type
- string: `let strname="name"`
    > combine string: `str1` + `str2`
- Integer `let age= 20`
- boolean: `let boolname=true'
- undefined type: 空直
    > value that is not assign
    >> ex:
    ```
    let test
    console.log(test) //undefined
    let bag = undefined
  ```
- Null Type:空直
    > empty or unknow value，null 不等 undefined
    >> ex:
    >>`let bag = null`


## 3.  condition statement
### if else
```
const num= -5

if (num > 0){
console.log("num is positive")
}
else if( num < 0 ){
console.log("Number is negative")
}
else(
console.log("Number is zero")
)
```
> **output**
>> Number is negative

### SWITCH
> switch(key){
> case value
> } 

```
let key=900

switch(key){
case 100:
console.log("key 100")
break;

case 200:
console.log("key 200")
break;

default:
console.log("no score")
break;
}
```

## 4. loop
### for loop
```
for (let i=0; i<10; i++){
console.log("i:", i)
}
```
> **output:**
>> we can also use : `i++` or `i+=2`

#### array with for loop

##### Example1: loop in array 
```
const numArray=[1,2,3,4,5]
for (const num of numArray){
console.log("iteration number " + num)
}
```
> **output:**
>> iteration number 1
>> iteration number 2
>> iteration number 3
>> iteration number 4
>> iteration number 5

##### Example2: 
```
let classA = ['80','90','50']
for (let i = 0; i < classA.length; i++){
if (i ===2){
classA[i]=900
}
console.log("i:",classA[i])
}
```
> **output:**
>> i: 80
>> i: 90
>> i: 100


#### object with for loop
```
const posts = [
{
name: 'Mary',
desc: 'Hello Mary', 
},
{
name: 'Anna',
desc: 'Hello ANNA', 
},
]

for (let i =0; i< posts.length;i++)
{
if (i ===1){
let post = posts[i];
console.log(post)
}
}
```
> **output:**
>> `{ name: 'Anna', desc: 'Hello ANNA' }`
 
### While
```
let condition= true
while(condition){
console.log('....')
}
```

#### while only true will execute
```
let i = 1
while(i <=5){
console.log('iteration' + i)
i++
}
```
> **output:**
>> iteration number 1
>> iteration number 2
>> iteration number 3
>> iteration number 4
>> iteration number 5

#### condition stop when traget match
```
let condition= true
let target = 10
let i =0

while(condition){
if (i === target){
condition= false
}
console.log(i)
i++
}
```
> **output:**
>> 0
>> 1
>> 2
>> 3
>> 4
>> 5
>> 6
>> 7
>> 8
>> 9
>> 10

### do while loop
```
let i = 1
do {
console.log('iteration ' + i)
i++
} while (i <=5)
```
> **output:**
>> iteration number 1
>> iteration number 2
>> iteration number 3
>> iteration number 4
>> iteration number 5

###  3. array
- decalare array: 

    > ex1:
    >> `let arrayName=['a','b','c']`

    > ex2: 
    >> `const oddNumber=[1,3,4,5,7]`
    >> `console.log(oddNumber[0])`

- push加值: 
> `arrayName.push('value')`

- length長度: 
> `console.log(arrayName.length)`

- index:
> `array[0]`

###  4. object
> basic object 
>> ex
```= javascript
const person = {
firstName: 'Bruce',
lastName: 'Lee',
age:30,
}
console.log(person.lastName) 
```
> **output**
>> Lee

#### **example 1**
```
const post= {
  images: 'https://xx.img.com/a1.png',
  desc: 'this is a image',
  date: '2022/07/14',
  comment: ['awesome','cool','nicepic']  
}

const wall = [
  post,
  post,
  post,
]
console.log(wall)
```
> **output**
```
[
  {
    images: 'https://xx.img.com/a1.png',
    desc: 'this is a image',
    date: '2022/07/14',
    comment: [ 'awesome', 'cool', 'nicepic' ]
  },
  {
    images: 'https://xx.img.com/a1.png',
    desc: 'this is a image',
    date: '2022/07/14',
    comment: [ 'awesome', 'cool', 'nicepic' ]
  },
  {
    images: 'https://xx.img.com/a1.png',
    desc: 'this is a image',
    date: '2022/07/14',
    comment: [ 'awesome', 'cool', 'nicepic' ]
  }
]
```

####  **example2:**
continue above example, and add another post
```
const post2= {
  images: 'https://xx.img.com/a2.png',
  desc: 'this is a image',
  date: '2022/07/15',
  comment: ['awesome','cool','nicepic', 'wow']  
}

const wall = [
  post,
 post2,
]

console.log(wall)
```
> **output**
>> `createCard { name: 'Ma' }`
>> `createCard { name: 'Ma2' }`
>> `createCard { name: 'Ma3' }`

### 5 . operator
> `>` `<` `||` `&&` `!==`

```
let x=10
let y=20
console.log(x%y) //mod get remainder 
console.log(++x) //x=x+1
```

#### compare `==` and `===`
- `!` 把結果反向
>> ex: 
>> `const isValid = true`
>> `console.log(!isValid)` //false

- `==` vs `===`
> `==` 直比較 `x==y` //compare value, return bool
>>會幫你轉換想等data type
>> ex: `1 == "1"` //true

> `===` 嚴格判斷 `x===y`//compare value, and data type, return bool
>> ex: `1 === "1"` //false


#### string with operator
> `console.log('bruce '+ 'Lee')`
>> output:
>> `Bruce Lee`

#### tricky
```
const isEven = 10 % 2 ==0 ? true : false
console.log(isEven)
```
If 10%2 ==0 , true or flase assign to isEven
> **output:**
>> true

```
const isEven = 10 % 2 ==0 ? 'Number is Even ' : 'Number is odd'
console.log(isEven)
```
> **output:**
>> Number is Even


#### conversions
> concatenation
>> `console.log(2 + '3')` // 23
>> `console.log(true+'3')` //true3

> opertion will convert to number
>> `console.log('4'- '2')` //2
>> `console.log('lee' - 'ted')` //nam not a number
>> `console.log(parseFloat('3.14'))`
>> `console.log(String('500'))` 
>> `console.log(500).toString()`

### 6. function
#### basic function
```
function hello(){
console.log('你好')
}
hello()
```
> `你好`

#### function with value
```
function addMoney(price1, price2, discount){
console.log(price1+price2 + discount)
}

addMoney (400, 500) //沒放第3參數會出現undefine。JS不嚴謹 
addMoney (600, 700, 100)
```
> **output:**
>> NAN
>> 1400

#### function return value
```
function addMoney(price1, price2, discount){
let result = price1+price2 -discount
return result
}


let total = addMoney (400, 500, 50)
console.log('total', total)
addMoney (600, 700, 100)
```
> **output:**
>> total 850

#### function return and if else
```
function addMoney(price1, price2, discount){
let result = price1+price2 -discount
let message= "normal account"

if (result > 20000){
message= "platinum account"
return message
}
if (result > 50000){
message= "VIP"
return message
}

return message
}


let message= addMoney (11000, 500000, 50)
console.log('msg', message)
```
> **output**
>> msg platinum account
 
#### 構造函數constructor Function
```
function createCard(initName){
this.name=initName

}

const a1 = new createCard("Ma")
const a2 = new createCard("Ma2")
const a3 = new createCard("Ma3")
const a4 = new createCard("Ma4")
const a5 = new createCard("Ma5")
console.log(a1)
console.log(a2)
console.log(a3)
```
> **output**
>> createCard { name: 'Ma' }
>> createCard { name: 'Ma2' }
>> createCard { name: 'Ma3' }

#### array function `=>`

> `function hello(){}`
> `let hello = function (){}`
>> shorthand
>> `let hello = () =>{}`


```
#method1
const arrowSum = (a , b) => {
  return a+b
}

const sum1 = arrowSum (30, 40)
console.log(sum1)

# method 2
const arrowSum2=(a, b) =>a+b
const sum2 = arrowSum2 (30, 40)
console.log(sum2)
}

```

## DOM