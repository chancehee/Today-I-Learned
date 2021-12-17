### 20211218  

### 로또추첨기 어플  
내가 지정한 숫자를 포함하며, 포함하지 않는 나머지 숫자는 랜덤하게 숫자를 생성하는 어플이다.  

### 사전 지식  
#### 1. Collection 자료형  
set(집합), list(목록), map(매핑개념: key,value 구조) 자료형이 있으며 변경가능한 자료형과 변결불가능한 자료형으로 나눌수 있다.  
isEmpty() 함수를 통해 값이 있으면 True 없으면 False를 반환하는 등 여러 기능을 가진 함수를 사용 가능하며  
값을 추가 할때는 .add() 를 통하여 추가한다.



#### 2. Random 함수  
fun Random(seed : Int) : Random  
// Random 함수를 살펴보면 seed를 설정할 수 있다.   
이 경우 랜덤의 수가 이미 정해진 순서로 나오기 때문에, 랜덤하게 구현하려면 seed를 시간으로 해주면 랜덤하다.  

#### Random 함수 사용 예)  
```kotlin
val random = Random()
// nextInt() 함수를 통하여 바운드를 지정해줄 수 있다. 이 경우 0~44로 범위 지정 +1을 통해 1~45의 값을 가져온다.
print("${random.nextInt(45) + 1}")

// 6개의 수를 가져올 경우 6번 반복 (중복이 생길 수도 있다.)
for (i in 1..6){
    println("${random.nextInt(45) + 1}")
}

// 중복을 방지하는 3가지 방법
// 1. 리스트로 중복확인하기
val list = mutableListOf<Int>()
while (list.size < 6){
    val randomNumber = random.nextInt(45) + 1
    // contatins() 함수를 통하여 Boolean 값 반환
    if (list.contains){
        continue
    }
    list.add(randomNumber)
}
print(list)

// 2. 집합 자료형 사용하기
val numberSet = mutableSetOf<Int>()
while (numberSet.size < 6){
    val randomNumber = random.nextInt(45) + 1
    numberSet.add(randomNumber)
}
print(numberSet)


// 3. 45개 숫자 생성후 shuffle하고 앞 6개만 잘라서 사용하기
// apply 함수를 통하여 초기화 진행 
val list = mutableListof<Int>().apply{
    for (i in 1..45){
        this.add(i)
    }
}
list.shuffle()
// subList(from, to) 함수를 활용하여 list의 앞 6자리만 잘라서 사용하기
print(list.subList(0,6))


```

### 배운 내용 정리  
collection 자료구조에 대한 전반적인 개념과 쓰임을 공부하였고, Random() 함수의 사용법(nextInt()) , contains() 함수, subList(from,to) 함수를 공부 하였다.
