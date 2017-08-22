# template string
`'`나 `"`와 같은 따옴표 대신 백틱 문자인 `` ` ``를 사용한다.
```javascript
const backtick = `'single quotes'와 "double quotes" 혼용 가능`;
```
여러 줄에 걸쳐 문자열을 작성할 수 있다.
```javascript
const template = `<ul class='nav'>
    <li><a href='#home'>Home</li>
</ul>`;
```
\+ 연산자를 사용하지 않아도 문자열을 삽입할 수 있다.
```javascript
const year = '2017';
const month = '08';
const day = '22';

// 기존에는
console.log('Today is ' + year + '-' + month + '-' + day);

// ES2015
console.log(`Today is ${year}-${month}-${day}`);
```
`${expression}`에는 자바스크립트 표현식도 사용할 수 있다.
```javascript
console.log(`1 + 1 = ${1 + 1}`);
const name = 'youngeun';
console.log(`HELLO, ${name.toUpperCase()}`);
```