# const
## 선언과 초기화
1. 초기화 이후 재할당이 금지된다.
```javascript
const C = 1;
C = 2;                  // TypeError: Assignment to constant variable.
```
2. 반드시 선언과 동시에 초기화가 이루어져야 한다.
```javascript
const C;    // SyntaxError: Missing initializer in const declaration
```
3. Block-level scope를 갖는다.
```javascript
{
    const C = 1;
    console.log(C);     // 10
}
console.log(C);         // ReferenceError: C is not defined
```
## 상수
```javascript
// Low readability
if (x > 10) { ... }

// Better
const MAXROWS = 10;
if (x > MAXROWS) { ... }
```
## 객체
- 참조의 변경은 금지하지만, 객체의 내용(프로퍼티)는 변경이 가능하다.
- 객체 타입 변수 선언에는 const를 사용하는 것이 좋다
    + 어짜피 객체의 참조가 변경될 일이 없음. 새로운 참조가 필요하면 새로운 변수 사용하면 됨.
```javascript
const user = {
    name: 'youngeun',
    address: {
        city: 'Suwon'
    }
};

user = {};              // TypeError: Assignment to constant variable.

user.name = 'ye';

console.log(user);      // { name: 'ye', address: { city: 'Suwon' } }
```