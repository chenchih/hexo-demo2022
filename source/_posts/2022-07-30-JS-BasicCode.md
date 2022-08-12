---
title: JS Basic Code 基本
date: 2022-07-30 07:59:48
tags: JS
categories:
- [WebDev, CSS]
---

## JS基本須知道

### How to run JS
- Browser- inspect
    - Method1:
    > Go to inspect > console

    - Method 2:
    > inspect> sources> snipperts> create js file

- NodeJS environment

    > 寫 `XXX.js`//CREATE JS file
    >> `node XXX.js` //run .js file using node

### adding comment
`//` single line comment
`/**/`: multiply line comment

### 顯示 print
- `console.log()` 顯示在console
- `alert()` 跳出顯示
- `document.write("\<h1>hello <br\/>")`

## JS　 基本語法- Part 1
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
#### string:
##### declare String and print string
```
name="Jessie"
console.log( 'Hello', name); //Before ES5
console.log( `Hello, ${name}!` ); // After Es6
```

##### combind two String
```
strname="hello"
str2name="world"
console.log(strname + " " + str2name)
```
##### template literals (concatenate strings)(ES6)
> before ES6:
>> var message = 'Hello ' + name;

> After ES6 using the \```${}``\`
>> const message_new = `Hello ${name}`;
>> console.log(`3! is ${3*2*1}`);
>> console.log(`${1+2+4}`);

##### Ex:
```
//example1:
var name = 'World';
var message = 'Hello ' + name; //before ES6
console.log(message);

const message_new = `Hello ${name}`; //after ES6
console.log(message_new);

//example2:
let name = "Ilya";
console.log( `hello ${1}` ); // hello 1
console.log( `hello ${"name"}` ); // hello name
console.log( `hello ${name}` ); // hello Ilya
```

#### number
> `let age= 20`

#### boolean:
>`let boolname=true`

#### undefined type: 空直
> value that is not assign
##### Ex:
```
  let test
  console.log(test) //undefined
```

#### Null Type:空直
> empty or unknown value，null 不等 undefined

##### Ex:
let age = null;
console.log(age)

#### `typeof` check data Type
> typeof

- example types:
> typeof undefined // "undefined"
> typeof 0 // "number"
> typeof 10n // "bigint"
> typeof true // "boolean"
> typeof "foo" // "string"
> typeof Symbol("id") // "symbol"
> typeof Math // "object"  (1)
> typeof null // "object"  (2)
> typeof alert // "function"  (3)

##### Ex:
```
let hellostr="hello";
let num = 123;
console.log(typeof(hellostr) )//String
console.log(typeof(num)) //number
```

### 3. Interaction: alert, prompt, confirm
- `alert`: pop up and shows a message.
- `prompt`: shows a message asking the user to input text.
  - It `returns the text` or, if `Cancel button` or `Esc` is clicked, `null`.   
- `confirm`: shows a message and waits for the user to press “OK” or “Cancel”.
  - It `returns true` for `OK` and `false` for `Cancel/Esc`.

#### Example:
```js=
//prompt and alert
let age = prompt('How old are you?', 100);
alert(`You are ${age} years old!`); // You are 100 years old!

//confirm and alert
let isBoss = confirm("Are you the boss?");
alert( isBoss ); // true if OK is pressed
```


### 4. Type Conversions
#### String Conversion
- string to number convert
```
let value = "123";
console.log(typeof value); // string
value = Number(value); // now value is a number
console.log(typeof value); // number
```

#### Numeric Conversion
- number to string convert: `toString`
```
let num=500;
console.log(typeof(num))
convertstr= num.toString()
//or convertstr= String(num)
console.log(typeof(convertstr))
```
### 5. operator
> `>` `<` `||` `&&` `!==`

#### remainder %
```
let x=10
let y=20
console.log(x%y) //mod get remainder
console.log(++x) //x=x+1
```

#### Exponentiation **
The exponentiation operator a ** b raises a to the power of b.
> console.log( 2 ** 2 ); // 2² = 4
> console.log( 2 ** 3 ); // 2³ = 8
> console.log( 2 ** 4 ); // 2⁴ = 16

#### String concatenation with binary +
- using `+` to concatenate string
```
let s = "my" + "string";
console.log(s) // mystring
```
-  `+` to concatenate a string  and number
Note: if any of the operands is a string, then the other one is converted to a string too
```
str1= '1' + 2
str2=  2 + '1'
console.log( typeof(str1) ); // string
console.log( typeof(str2)); // string
```

- complex example
> console.log(2 + 2 + '1' ); // "41" and not "221"
>> the first two number add together and then add 1, so it will look like this: 4+'1'=>41

> console.log('1' + 2 + 2); // "122" and not "14"
>> Here, the first operand is a string, the compiler treats the other two operands as strings too.

- other arithmetic operators
binary + is the only operator that supports strings in such a way. Other arithmetic operators will convert string to Number
> console.log( 6 - '2' ); // 4, converts '2' to a number
> console.log( '6' / '2' ); // 3, converts both operands to numbers

#### Numeric conversion, unary + (convert str to number)
It actually does the same thing as Number(...), but is shorter. In above convert we use Number(...),we can also use `+`to convert.

```
// No effect on numbers
let x = 1;
console.log( +x ); // 1

let apples = "2";
let oranges = "3";
console.log( apples + oranges ); //23 string
// both values converted to numbers before the binary plus
console.log( +apples + +oranges ); // 5 covnert to number
```
#### Chaining assignments '='
Chained assignments evaluate from right to left.
```
let a, b, c;
a = b = c = 2 + 2;
console.log( a ); // 4
console.log( b ); // 4
console.log( c ); // 4
```
without cain your code have to write pretty long like this:
```
c = 2 + 2;
b = c;
a = c;
```

#### Increment/decrement
- counter++: `counter=counter+1`
- counter--: `counter=counter=1`

### 6. Comparisons
#### `!` 把結果反向
>> ex:
>> `const isValid = true`
>> `console.log(!isValid)` //false

#### Strict equality  `==` and `===`
- For a non-strict check `==`
> `==` 直比較 `x==y` //compare value, return bool
>>會幫你轉換想等data type
>> ex: `1 == "1"` //true

- For a strict check `===`
> `===` 嚴格判斷 `x===y`//compare value, and data type, return bool
>> ex: `1 === "1"` //false

> alert( null == undefined ); // true
> alert( null === undefined ); // false

#### null vs undefined vs 0
- null vs 0
> console.log( null > 0 );  // (1) false
> console.log( null == 0 ); // (2) false
> console.log( null >= 0 ); // (3) true

- undefined vs 0
> console.log( undefined > 0 ); // false (1)
> console.log( undefined < 0 ); // false (2)
> console.log( undefined == 0 ); // false (3)

### 7 condition if & ? statement
#### if else if else
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
#### if (0) Boolean conversion
- false will never execute
```
if (0) { // 0 is falsy
  ...
}
```
- true will execute
```
if (1) { // 1 is truthy
  ...
}
```

#### ? operator
>syntax: let result = condition ? value1 : value2;

##### Ex1: If else and  ?  
```
let accessAllowed;
let age = prompt('How old are you?', '');
if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}
alert(accessAllowed);
```
Now we can use shorter way:  
```
let age = prompt('How old are you?', '');
let accessAllowed = (age > 18) ? true : false;
alert(accessAllowed);
```

##### ex2: boolean
- boolean
```
const isEven = 10 % 2 ==0 ? true : false
console.log(isEven) //true
```
- sting
```
const isEven = 10 % 2 ==0 ? 'Number is Even ' : 'Number is odd'
console.log(isEven) // Number is Even
```

##### ex3 prompt example:
- using if else
```
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```
- using ?
```
let age = prompt('age?', 18);
let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';
console.log( message );
```

##### ex3 prompt example:
- ? method
```
let company = prompt('Which company created JavaScript?', '');

(company == 'Netscape') ?
   alert('Right!') : alert('Wrong.');
```

- if else
```
let company = prompt('Which company created JavaScript?', '');

if (company == 'Netscape') {
  alert('Right!');
} else {
  alert('Wrong.');
}
```
### 3. function
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



## JS　 基本語法- Part 2 loop迴圈 and condition條件

### 1. loop
#### for loop
- Syntax:
```
for (begin; condition; step) {
  // ... loop body ...
}
```
#### Example:
- for loop
```
for (let i=0; i<10; i++){
console.log("i:", i)
}
```
> **output:**
>> we can also use : `i++` or `i+=2`

- step by step
```
// for (let i = 0; i < 3; i++) alert(i)

// run begin
let i = 0
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// ...finish, because now i == 3
```

### While
```
let condition= true
while(condition){
console.log('....')
}
```

#### Ex1: while only true will execute
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

#### Ex2 condition stop when traget match
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
do {
  // loop body
} while
```
#### ex1:
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



## JS　 基本語法- Part 3 array object class
###  1. array
#### decalare array:
##### ex1:
- decalare array with value
```
let arrayName=['a','b','c']
console.log(arrayName) //[ 'a', 'b', 'c' ]
const oddNumber=[1,3,4,5,7]
console.log(oddNumber[0]) //1
console.log(oddNumber[4]) //7
```
- Trailing comma
```js=
let fruits = [
  "Apple",
  "Orange",
  "Plum",
];
```
- replace new element
> fruits[2] = 'Pear'; // now ["Apple", "Orange", "Pear"]

- decalare empty array:
We can use either way to create empty array
>let arr = new Array();
> let arr = [];

#### length長度:
> `console.log(arrayName.length)`

#### Method push pull shift
- push加值 appends an element to the end.
> `arrayName.push('value')`

- pop takes an element from the end.
> `arrayName.push('value')`

- shift: get an element from the beginning, advancing the queue, so that the 2nd element becomes the 1st.


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

###  2. object
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

## reference
- https://javascript.info/
