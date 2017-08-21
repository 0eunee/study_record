# let
## Block-level scope
- ES2015 이전
```javascript
var i = 1;
console.log(i);     // 1
{
    var i = 2;
}
console.log(i);     // 2
```
- ES2015
```javascript
let i = 1;
{
    let i = 2;
    let j = 2;
}
console.log(i);     // 1
console.log(j);     // ReferenceError: j is not defined
```
## 중복 선언 금지
```javascript
var i = 1;
var i = 2;      // OK

let j = 1;
let j = 2;      // Uncaught SyntaxError: Identifier 'j' has already been declared
```
## TDZ(Temporal Dead Zone)
`var`변수는 등록과 초기화가 한번에 이루어지지만(호이스팅), `let`변수는 등록은 되지만 초기화는 선언문에 도달했을 때(선언문에 도달하기 전까지는 TDZ에 존재) 이루어진다. 
```javascript
console.log(i);     // undefined
var i;
console.log(j);     // Error: Uncaught ReferenceError: j is not defined
let j;
```
## 클로저
```javascript
var funcs = [];

for (var i = 0; i < 3; i++) {
    funcs.push(function () { console.log(i); });
}

for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```
위 코드는 0, 1, 2를 기대하지만 결과는 `i`가 전역변수이기 때문에 3이 세번 출력된다. 따라서 아래와 같이 클로저를 활용한 코딩이 필요하다.
```javascript
var funcs = [];

for (var i = 0; i < 3; i++) {
    (function (index) {
      funcs.push(function () { console.log(index); });
    }(i));
}

for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```
하지만 ES2015의 `let`키워드를 사용하면 동일한 동작을 한다.
```javascript
var funcs = [];

for (let i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

for (var j = 0; j < 3; j++) {
  funcs[j]();
}
```
## Not Global Object's property
`let`변수는 보이지 않는 개념적인 블럭 내에 존재한다.
```javascript
var i = 1;
console.log(window.i);      // 123

let j = 1;
console.log(window.j);      // undefined
```