# ajax 응답 중 새로고침 시 발생하는 error 방지하기
```javascript
$.ajax({
  /* ajax options omitted */
  error: function (xmlHttpRequest, textStatus, errorThrown) {
    if(xmlHttpRequest.readyState == 0 || xmlHttpRequest.status == 0) {
      return;  // it's not really an error
    } else {
      // Do normal error handling
    }
});
```
---
- 출처: http://fedev.tistory.com/13
