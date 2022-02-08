### 20220208  

### COUNT() 함수  
- 요약: SELECT 쿼리로 반환된 결과의 개수를 반환한다.
- 문법: COUNT(칼럼)
- 특징: NULL 값은 0으로 센다. COUNT내부에 조건문도 가능하다.

```sql
# 테이블에서 모든 행의 개수 세기
SELECT COUNT(*) FROM 테이블

# 테이블에서 특정 열의 데이터의 개수 세기
SELECT COUNT(칼럼) FROM 테이블

# 테이블에서 중복이 없는 특정 열의 데이터의 개수 세기
SELECT COUNT(DISTINCT 칼럼) FROM 테이블
```
