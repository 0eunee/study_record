# 자바 전 월 날짜 구하기
2018년도를 맞이하여 기존 날짜 코드가 오류를 뱉기 시작했다.  
보고서 조회 쪽이 기본 한 달로 잡혀 있는 기간 조회의 형식인데, 한달 전 날짜가 **2017년 12월**로 나오는 것이 아니라 **2018년 00월**과 같이 이상하게 나오고 있었다.  
코드를 보니 년도가 바뀌는 것을 고려하지 않았는지 아무런 조치가 없었고, 전 월 또한 `calendar.get(calendar.MONTH)` 로만 되어 있었다.  
월은 아마 현재 월이 `calendar.get(calendar.MONTH) + 1` 이니까 전 월은 `+1`이 없으면 된다고 생각했나 보다.  

그래서 구글링을 한 후 아래와 같이 바꾸었다.
```java
Calendar calendar = Calendar.getInstance();

// 오늘
int year = calendar.get(calendar.YEAR);
int month = calendar.get(calendar.MONTH) + 1;
int day = calendar.get(calendar.DATE);

String date = year + "-" + (month < 10 ? "0" + month : month) + "-" + (day < 10 ? "0" + day : day);
model.addAttribute("curDate", date);

// 한달 전
calendar.add(calendar.MONTH, -1);   // 한달 전으로 슝!!!
year = calendar.get(calendar.YEAR);
month = calendar.get(calendar.MONTH) + 1;
day = calendar.get(calendar.DATE);

date = year + "-" + (month < 10 ? "0" + month : month) + "-" + (day < 10 ? "0" + day : day);
model.addAttribute("lastDate", date);
```
