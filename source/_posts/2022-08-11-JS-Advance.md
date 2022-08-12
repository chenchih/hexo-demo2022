---
title: JS Advance
date: 2022-08-11 13:00:48
tags: JS
categories:
- [WebDev, CSS]
---
## Advance JS

### 構造函數constructor Function
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

### array function `=>`
In ES6 there is a new function called array function, which you can write shorter function.

> Before ES6
>> function hello(){}

> after ES6
>> let hello = function (){}
>> shorthand
>> let hello = () =>{}

#### function without passing paramter
> Before ES6 (normal function)
>> ex: function hello(){}
```
function test(a ,b){
console.log(a, b)
}
test('hello', 'world');
```

> ES6 arrow function:
>> ex: let hello = () =>{}
```
const test =(a,b) => {console.log(a, b)}
test('hello', 'world');
```

#### function with passing varable and return
> Before ES6 (normal function)
>> ex:
```
function arrowSum (a , b)  {
    return a+b
  }
console.log(arrowSum(5,6))
```

> ES6 arrow function:
>> example
>> function=()=>{return } //with return
>> function=()=> // Single line arrow function
```
arrowSum=(a,b)=>{
return a+b
}
// or arrowSum=(a, b) =>a+b
console.log(arrowSum(5,6))
```
We can either add return or not. Without return we call it `implicit return`; values are returned without having to use the return keyword.


## reference
- https://javascript.info/
