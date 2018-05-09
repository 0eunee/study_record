# identity 사용하기
```sql
-- insert한 identity값 불러오기
insert into () values () select @@Identity;

-- ID 증가값 수동으로 넣겠다
SET IDENTITY_INSERT [테이블명] ON;
-- ID 증가값 자동으로 넣겠다
SET IDENTITY_INSERT [테이블명] OFF;
```
