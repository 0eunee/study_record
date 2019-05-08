# 함수 파라미터 공백값 오류 처리
`<tr onclick="fn_abcd(param1, param2)">..</tr>` 요런 코드를 만들어 html쪽으로 붙이는 스크립트가 있었는데, `param2`의 값으로 `1 234 4567 8`가 들어오니  
html쪽에서는 `<tr onclick="fn_abcd('aa', '1')">..</tr>` 이런 식으로 파라미터가 잘려서 나오더라.  
```javascript
'aa bb cc'.replace(/ /gi, '&nbsp;');
```
공백을 치환하면 정상적으로 동작!
