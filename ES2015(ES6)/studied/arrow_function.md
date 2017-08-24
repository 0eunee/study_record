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