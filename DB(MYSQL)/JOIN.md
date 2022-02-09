### 20220209  

## JOIN  
![JOIN(MYSQL)](https://user-images.githubusercontent.com/59447235/153201068-0b06b27b-6c04-4923-b397-27b3a954090e.png)  

- 요약: '참여하다' 라는 뜻으로 DB에서는 두 개 이상의 테이블이나 데이터베이스를 연결하는 것이다. 
검색 하고 싶은 값들이 두 개 이상의 테이블에 있을 경우, 한개의 테이블로 JOIN 시킨 후, 결과를 가져오는 연산을 수행한다.
보통의 경우는 KEY를 가지고 두 개의 테이블을 연결한다.
- 종류: 등가 조인, 비등가 조인, 자체 조인, 교차 조인, 외부 조인
- 형식: SELECTE 테이블1.칼럼, 테이블2.칼럼 FROM 테이블1 LEFT JOIN 테이블2 ON 테이블1.KEY = 테이블2.KEY  
(조인의 종류가 많지만 그중에서 빈번하게 사용하는 LEFT JOIN을 형식으로 적어봤다.)
- 특징: 해당하는 칼럼의 값이 없다면 NULL로 적힌다.
- Q.순수 테이블1 값만 뽑고 싶다면?  
테이블1으로 LEFT JOIN 후에 WHERE 테이블2.ID IS NULL 구문을 통해서 뽑아 올 수 있다.  

```sql
# 테이블 A,B가 존재 할 때, A 테이블에 포커스를 두고 B 테이블을 JOIN 시켜준다.
SELECT A.ID, A.NAME, B.ID, B.NAME
FROM A
LEFT JOIN B ON A.KEY = B.KEY
# 순수 A 테이블만 추출
WHERE B.ID IS NULL
```
