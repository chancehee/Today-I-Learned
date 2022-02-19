### 20220219  

## SET  
- 요약: DB에서, 사용자 정의 변수 선언 및 초기화할 때 사용한다.
- 형식: SET @변수이름 = 대입값; 혹은 SET @변수이름 := 대입값;  
- 특징:   
SET 이외의 명령문에서는 =가 비교연산자로 취급되기 때문에 SELECT로 변수를 선언하고 값을 대입할 때는 :=를 사용한다.  
저장하는 값에 의해 자료형이 정해지며, Integer, Decimal, Float, Binary 그리고 문자열 타입만 취급 가능하며, 변수를 초기화 하지 않은 경우 값은 NULL, 자료형은 String 타입이다.  

```sql

/* 변수명이 HOUR이고 값을 -1로 초기화 한다. */
SET @HOUR = -1;

/* 테이블 행의 수만큼 변수에 1를 더하는 연산을 반복한다.  */
SELECT (@HOUR := @HOUR + 1) AS HOUR FROM 테이블;

/* 프로그래머스, 입양 시각 구하기(2) 문제 풀이 */
/* 보호소에서 입양이 발생하는 건수를 시간대 별로 몇건이 존재하는지 조회하기. */
SET @HOUR = -1
SELECT (@HOUR := @HOUR + 1) AS HOUR, 
(
SELECT COUNT(*)
FROM ANIMAL_OUTS
WHERE @HOUR = HOUR(DATETIME)
)
FROM ANIMAL_OUTS
WHERE @HOUR < 23;

```
