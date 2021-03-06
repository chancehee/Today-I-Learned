### 20220217  

## 서브 쿼리  
- 요약: 하나의 SQL문 안에 포함되어 있는 또 다른 SQL문을 말한다.   
(서브쿼리는 메인쿼리가 서브쿼리를 포함하는 종속적인 관계이다.)  
- 형식: SELECT * FROM 테이블 WHERE 칼럼 [IN(다중행), =(단일행)] (서브쿼리)
- 특징:  
1. 서브쿼리는 메인쿼리의 칼럼을 모두 사용할 수 있지만, 메인쿼리는 서브쿼리의 칼럼을 사용할 수 없다.  
2. 위치에 따라 서브쿼리를 사용할 수 있다.(사용가능한 위치: SELECT, FROM, WHERE, HAVING, ORDER BY, INSERT문의 VALUES, UPDATE문의 SET)  
3. ( ) 안에 서브쿼리를 적어줘야한다.  
4. 단일 행 또는 복수 행 비교 연산자와 함께 사용 가능하다.  
5. 서브쿼리에서는 ORDER BY를 사용하지 못한다.  
- 종류: 단일행 서브쿼리, 다중행 서브쿼리, 다중칼럼 서브쿼리

```sql
/* SELECT 절에서 사용되는 서브쿼리 */
SELECT 칼럼1, 칼럼2, (SELECT 칼럼3 FROM 테이블 [WHERE 절] ) 
FROM 테이블

/* FROM 절에서 사용되는 서브쿼리 */
/* 필요한 부분만 가져오는 테이블을 임시적인 뷰로 생성하여 사용한다. */
SELECT 테이블1.칼럼1, 테이블2.칼럼2 FROM 테이블1, (SELECT * FROM 테이블1 [WHERE 절])

/* WHERE 절에서 사용되는 서브쿼리 */
SELECT 칼럼1 FROM 테이블
/* 1.단일칼럼인 경우 '=' 사용 */
WHERE 칼럼2 = (SELECT 칼럼2 FROM 테이블 [WHERE 절]) 
/* 2.다중칼럼인 경우 'IN' 사용 */
WHERE 칼럼2 IN (SELECT 칼럼2 FROM 테이블 [WHERE 절])
```
