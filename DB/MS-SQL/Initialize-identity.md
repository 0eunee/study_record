# 자동 증가값 초기화하기
```sql
-- 시작값에 0을 넣으면 다음 값은 1부터!
DBCC CHECKIDENT ('[테이블명]', RESEED, 시작값);
```
