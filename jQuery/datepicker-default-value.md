# datepicker 오늘 날짜를 기본값으로
`setDate`나 `defaultDate`를 사용하는 방법도 있겠지만 나는 아래의 방법을 사용했다.
```javascript
$('input태그').val($.datepicker.formatDate('yymmdd', new Date()));
```
