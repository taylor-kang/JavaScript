# Grammer and Types

## Basics

---

JavaScript는 Java, C, C++의 많은 문법을 가져왔지만 Awk, Perl, Python 과 같은 언어의 영향을 받기도 하였습니다.

- JS는 case-sensitive하며 character set은 Unicode를 사용합니다.

```javascript
// Früh 선언가능
var Früh = "foobar"; 

//Case-sensitive
Früh != früh;
```

- JS에서 명령어는 statements라 불리고 semicolons(;)으로 구분합니다.
        - 하나의 statement가 한 라인에 쓰여져 있다면  semicolon은 필수는 아니지만, 한 개 이상의 statement가 하나의 라인에 선언 되어있다면 반드시 semicolon으로 분류되어야 합니다.
        
⇒ 하지만 statement뒤에 semicolon을 무조건 붙여 버그 발생 가능성을 줄입시다!

## Comments 주석

---

- 주석은 C++ 과 같습니다.
```javascript
// a one line comment

/*this is a longer,
*multi-line comment
*/

/* /*nested comments*/ */ SyntaxError
```
## Declarations 변수 선언

---

`var`

- function-scope
- execution-context(실행타임)에 scope 결정 **local** / **global**
- no assign → `undefined`

`let`

- block-scope
- local variable
- no assign → `undefined`

`const`

- block-scope
- local variable
- read-only 상수
- constant 이름은 같은 scope내의 함수명이나 다른 변수명과 갖게 선언 할 수 없습니다.
```javascript
// 선언 방법
const PI = 3.14;

// Error Case 1. 함수명과 같은 경우
function f() {}; 
const f = 5;

// Error Case 2. 다른 변수명과 같은경우
function f() {
        const g = 5; // error
        var g;
}

// const로 선언된 Object의 프로퍼티는 수정이 가능합니다.
const MY_OBJ = {'key': 'value'};
MY_OBJ.key = 'othervalue';

// const로 선언된 array는 수정이 가능합니다.
cosnt MY_ARRAY = ['HTML', 'CSS'];
MY_ARRAY.push('JS'); // MY_ARRAY = ['HTML', 'CSS', 'JS'];
```
### JS identifier rule

- start with letter / underscore(_) / dollar sign($)
- digits(0-9), uppercase character('A' - 'Z'), lowercase character('a' - 'z')
- unicode letters
- ex. `Number_hits` `temp99` `$credit` `_name`

### variable rule

- `undefined` value 는 `if` statement 에서 `false` 처럼 행동합니다.
```javascript
var myArray = [];
if(!myArray[0]) myFunc();
```
- `null` value는 numeric으로는 `0`의 값을 가지고, boolean으로는 `false` 값을 가집니다.
```javascript
var n = null;
console.log(n * 32); // will log0
```
## Variable Scope 변수 범위

---

### Function Scope variable

- **global variable** 전역 변수
    - 함수 밖에 선언된 변수
    - 이 변수는 코드 어디서든 사용 할 수 있습니다.
    - Global variable은 **global object**의 프로퍼티입니다. 웹페이지에서 global object는 `window` 이고, `window.variable` 에서 선언한 global variable을 찾을 수 있습니다.
    - 또한 다른 window나 frame안에 변수를 선언하여 사용할수 있습니다.
    ex. `parent.phoneNumber`
- **local variable** 지역 변수
    - 함수 안에 선언된 변수
    - 이 변수는 함수 안에서만 사용 할 수 있습니다.

### Block Scope variable

- ECMAScript2015 이전의 JS는 block statemet scope를 가지지 않았습니다.
- ECMAScript2015 부터는 `let` 을 통해 block scope `{}` 을 가지게 되었습니다.
```javascript
if(true){
        var x = 5;
        let y = 5;
}
console.log(x); // x is 5
console.log(y); // ReferenceError: y is not defined
```
## Hoisting 호이스팅

---

### Variable Hoisting 변수 호이스팅

- JS의 변수가 함수 혹은 statement의 맨 위로 올려져, 즉 "hoisted" 되어 선언되는 것.
```javascript
var myvar = 'my value';

(function() {
        console.log(myvar);
        var myvar = 'local value';
}) ();

// After hoisting
// 가장 가까이 있는 변수를 참조하게 되므로 gloabal 변수인 myval이 아닌 local 변수인 myval을 참조함. 
var myvar = 'my value';

(function() {
        var myvar;
        console.log(myvar); // undefined
        myvar = 'local value';
}) ();
```
- 하지만 호이스트 된 변수의 변수 할당부는 기존 위치에 남아있고, 변수 선언부만 올라갑니다.
    - `var` 는 할당부에서 `undefined` 값으로 initialize
    - `let` 과 `const` 는 initialize 되지 않음 → Reference Error 발생가능
```javascript
console.log(x); //ReferenceError
let x = 3;
```
### Function Hoisiting 함수 호이스팅

- **function declation**으로 정의된 함수는 호이스팅 됨
**function expression**으로 정의된 함수는 호이스팅 되지 않음.
```javascript
// Function Declaration
foo(); // "bar"
function foo() {
        console.log('bar');
}

// Function Expression
baz(); // TypeError: baz is not a function
var baz = function() {
        console.lof('baz');
};
```
## Data structure and Types

---

### Primitive data type (7개)

- **Boolean**.
    - `true` `false`
- **null**
    - JS는 case-sensitive 한 언어이므로 **Null, NULL** 과 같지 않습니다.
- **undefined**
    - 변수가 not defined 일 때 할당됩니다.
- **Number**.

    ex.  `42` 와 같은 integer 정수 / `3.1415` 와 같은 floating point 소수

- **BigInt**. 정밀한 정수를 표현할 때 사용합니다.

    ex. `9007199254740992n`

- **String**. charater의 연속인 text를 표현할 때 사용합니다.

    ex. `"Howdy"`

- **Symbol**
    - (new in ES6). unique하고 immutable한 인스턴스의 데이터 타입입니다.
- **Object**

### Data type conversion 데이터 타입변환

- JS는 동적 타입 언어입니다. 즉 변수를 선언할 때 데이터 타입을 명시하지 않아도 되며, 스크립트를 실행할 때 자동으로 데이터 타입이 변환 되기도 합니다.
```javascript
var answer  = 42;
answer = 'Thanks for all ther fish...'; //dynamically typed from Number to String
```
- 표현식내에 Numver 타입과 String 타입이 + 연산자로 연결되어 있을 경우, JS는 Number 타입을 String으로 변환합니다. + 가 아닌 다른 연산자에 관해서는, JS는 Number 타입을 String으로 변환하지 않습니다.
```javascript
x = 'The answer is ' + 42; // "The answer is 42"

'37' - 7 // 30
'37' + 7 // "377"
```
### Convert String to Numbers

- `parseInt(string, [radix])`
```javascript
parseInt("20") // 20
parseInt("20.00") // 20 : 소수점 이하는 버림.
parseInt("    50 ") // 50 : 공백은 제거됨
parseInt("1 20 40") // 1 : 여러 숫자가 주어질 경우 첫번째 데이터가 숫자면 변환
parseInt("50 나이") // 50: 숫자 문자 섞여 있을 떄, 첫번째 데이터가 숫자면 변환
parseInt("나이 50") // NaN: 숫자 문자 섞여 있을 떄, 첫번째 데이터가 문자면 에러 NaN 데이터 반환

// radix: optional parameter, default 10
parseInt("101",2) //5
```        

- `parseFloat()`
- `+` (unary plus) operator
```javascript
'1.1' + '1.1' // '1.11.1'
(+'1.1') + (+'1.1') // 2.2
+'1.1' + +'1.1' // 2.2 : 괄호 없이도 가능
```
## Literals

---

### Array Literals
```javascript
// []안에 , 로 구분합니다.
var coffees = ['French Roast', 'Colombian', 'Kona'];

// 모든 값을 표기하지 않아도 되지만, 값을 표시하지 않은 인덱스에는 undefined 값이 들어갑니다.
// 코드의 명확성을 높이기 위해서 undefined를 표기하는 것이 좋습니다.
var fish = ['Lion', , 'Angel']; //fish[1] = undefined, fish[2] = 'Angel'

// 하지만 마지막에 오는 콤마는 무시됩니다.
var myList = ['home', , 'school', ]; // myList[3] is not declared.
```
### Boolean Literals

- `true`
- `false`
- **Primitive Boolean** value vs **Boolean Object**

    Boolean object는 primitive boolean 데이터 타입을 감싼 객체입니다.

    참고) [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)

### Numeric Literals

`Number` 과 `BigInt` 타입은 10진수(decimal) , 16진수(hexa-dec), 8진수(octal), 2진수(binary) 로 표현할 수 있습니다.
```javascript
// decimal, base 10 
0, 117, -345, 123456789123456789n

// octal, base 8 : 앞에 0, 0o, 0O 를 표기하면 8진수
015, 0001, -0o77, 0o777777777777n

// hexadecimal, "hex" or base 16 : 앞에 0x, 0X 표기하면 16진수
0x1123, 0x00111, -0xF1A7, 0x123456789ABCDEFn

// binary, base 2 : 앞에 0b, 0B 표기하면 2진수
0b11, 0b0011, -0b11, 0b11101001010101010101n
```
### Floating-point Literals
```javascript
// Syntax
[(+|-)][digits].[digits][(E|e)[(+|-)]digits]

//ex.
3.1415926
-.123456789
-3.1E+12
.1e-23
```
### Object Literals
