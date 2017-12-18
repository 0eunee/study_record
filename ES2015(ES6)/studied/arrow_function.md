# Arrow function
## Syntax
function 키워드 대신 화살표(=>)를 사용하여 함수 선언
```javascript
// 매개변수 지정 방법
    () => { ... }   // 매개변수가 없는 경우  
     x => { ... }   // 매개변수가 한개인 경우(소괄호 생략 가능)
(x, y) => { ... }   // 매개변수가 여러개인 경우

// 함수 내용 지정 방법
x => { return x * x };
x => x * x;         // 한줄의 표현식이면 중괄호 생략 가능, 자동 return

() => { return { a: 1 }; };
() => ({ a: 1 });

() => {
    const x = 10;
    return x * x;
};
```
## 호출
Arrow function은 익명 함수로만 사용할 수 있어 호출하기 위해서는 함수표현식을 사용한다.
```javascript
// ES2015 이전
var multi = function (x) { return x * x; };
console.log(multi(10));

// ES2015
const multi = x => x * x;
console.log(multi(10));
```
또는 콜백함수로 사용한다.
```javascript
// ES2015 이전
var arr = [1, 2, 3];
var multi = arr.map(function (x) {
  return x * x;
});
console.log(multi);

// ES2015
const arr = [1, 2, 3];
const multi = arr.map(x => x * x);
console.log(multi);
```
## this
일반 함수의 경우, 함수 호출 패턴에 따라 `this`에 바인딩되는 객체가 달라짐. 콜백함수 내부의 `this`는 전역 객체 `window`를 가리킴
```javascript
function Prefixer(prefix) {
  this.prefix = prefix;
}
Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;
  });
};
var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));         // undefined Lee, undefined Kim
```
위의 결과로 `Hi Lee, Hi Kim`을 기대했겠지만, 두번째 함수의 `this`는 전역 객체 `window`를 가리키기 때문에 `undefined Lee, undefined Kim`이 출력된다.
```javascript
function Prefixer(prefix) {
  this.prefix = prefix;
}
Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;
  }.bind(this));
};
var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));         // Hi Lee, Hi Kim
```
## Arrow function의 this
Arrow function은 자신만의 `this`를 생성하지 않고 자신을 포함하는 외부 scope에서 `this`를 계승 받는다.
```javascript
function Prefixer(prefix) {
  this.prefix = prefix;
}
Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(x => `${this.prefix} ${x}`);
};
const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```
## Arrow function을 사용해서는 안되는 경우
1. 메소드
```javascript
// Bad
// 메소드를 호출한 객체에 this가 바인딩 되지 않고 전역 객체에 바인딩 됨
const obj = {
  name: 'Jeon',
  sayHi: () => console.log(`Hi ${this.name}`)
};
obj.sayHi();          // Hi undefined

// Good
const obj = {
  name: 'Jeon',
  sayHi() {   // === sayHi: function() {
    console.log(`Hi ${this.name}`);
  }
};
obj.sayHi();         // Hi Jeon
```
2. prototype
```javascript
// Bad
const obj = {
  name: 'Jeon'
};
Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);
obj.sayHi();         // Hi undefined

// Good
const obj = {
  name: 'Jeon'
};
Object.prototype.sayHi = function () {
  console.log(`Hi ${this.name}`);
};
obj.sayHi();        // Hi Jeon
```
3. 생성자
```javascript
const Temp = () => {};
// Arrow function은 prototype 프로퍼티가 없음
console.log(Temp.hasOwnProperty('prototype'));    // false
const temp = new Temp();        // TypeError: Temp is not a constructor
```
4. addEventListener 함수의 콜백 함수
addEventListener 함수의 콜백 함수를 화살표 함수로 정의하면 this가 상위 컨텍스트를 가리킴
```javascript
// Bad
var button = document.getElementById('myButton');
button.addEventListener('click', () => {
  console.log(this === window);   // => true
  this.innerHTML = 'Clicked button';
});

// Good
var button = document.getElementById('myButton');
button.addEventListener('click', function() {
  console.log(this === button);   // => true
  this.innerHTML = 'Clicked button';
})
```
