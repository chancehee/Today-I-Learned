### 20220214  

## LIMIT 연산자 
- 요약: 쿼리 결과 개수를 제한한다.
- 형식: LIMIT 개수(정수)
- 특징: 두 개의 정수가 들어간다면 (시작할 레코드의 번호, 시작부터 반환할 결과의 수)
ex) LIMIT 19,10 
20번 째 레코드에서 ~ 30번 째 레코드까지 검색한다.  

```sql
/* 처음레코드 index는 0이고, 1번째 부터 3개를 반환 한다.*/
LIMIT 3; 

/* 처음레코드 index는 19이고, 20번째 부터 10개를 반환 한다.(30번째 까지)*/
LIMIT 19, 10;
```
