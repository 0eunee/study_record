# 자바스크립트 전 월 날짜 구하기
2018년도를 맞이하여 기존 날짜 코드가 오류를 뱉기 시작했다.  
보고서 조회 쪽이 기본 한 달로 잡혀 있는 기간 조회의 형식인데, 한달 전 날짜가 **2017년 12월**로 나오는 것이 아니라 **2018년 00월**과 같이 이상하게 나오고 있었다.  
코드를 보니 년도가 바뀌는 것을 고려하지 않았는지 아무런 조치가 없었고, 전 월 또한 `getDate()` 로만 되어 있었다.  
월은 아마 현재 월이 `getDate() + 1` 이니까 전 월은 `+1`이 없으면 된다고 생각했나 보다.  

그래서 구글링을 한 후 아래와 같이 바꾸었다.
```javascript
var today = new Date();

// 오늘
var year = today.getFullYear();
var month = today.getMonth() + 1;
var day = today.getDate();
var curDate = year + '-' + ((month < 10) ? '0' + month : month) + '-' + ((day < 10) ? '0' + day : day);

// 한달 전
month = (new Date(today.getYear(), today.getMonth(), 0)).getMonth() + 1;
if (month == 12) { // 한달 전이 12월이면 작년이겠지!
  year -= 1;
}
var lastDayOfLastMonth = (new Date(today.getYear(), today.getMonth(), 0)).getDate();
if (day > lastDayOfLastMonth) {
  // 만약 오늘이 3월 31일 때, 2월 31일은 없으니까 그럴 경우에는 일자를 전 달의 마지막 날로 설정!
  day = lastDayOfLastMonth;
}
var lastDate = year + '-' + ((month < 10) ? '0' + month : month) + '-' + ((day < 10) ? '0' + day : day);
```
