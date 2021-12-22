### 20211222  

### 구현할 내용: 로또 번호 숫자의 범위에 따라 색상이 다른 공모양 배경을 설정해주기.(ShapeDrawable)  

### 0.XML 설정  
1. 글씨 색상을 white로  
2. TextView의 gravity를 center로  
```xml
<TextView
    android:id="@+id/TextView1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_margin="5dp"
    android:visibility="gone"
    tools:visibility="visible"
    android:gravity="center"
    android:textColor="@color/white"
    android:background="@drawable/circle_blue"
    android:text="1"
    android:textSize="18sp"
    android:textStyle="bold" /> 
```  
6개의 TextView(로또 번호)를 모두 위와 같이 설정 해주었다.  
  
  
### 1. drawable 파일 생성 (ShapeDrawable 사용하기)  
5가지 색상: 노랑, 파랑. 초록, 빨강, 회색  
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval"
    >

    <solid
        android:color="#D7C400"/>

    <size
        android:width="44dp"
        android:height="44dp"/>
</shape>
```  

### 2. drawable 파일 적용하기  
1. 하나씩 추가 할 때  
2. 자동 생성 할 때  
```kotlin
private fun initRunButton(){
        runButton.setOnClickListener {
            Log.d(TAG, "MainActivity - initRunButton() is called")

            // 인트 자료형 리스트 생성
            val list = getRandomNumber()

            list.forEachIndexed { index, number ->
                val textView = numberTextViewList[index]

                textView.text = number.toString()
                textView.isVisible = true
                
                // drawable 파일 적용하기
                number_bg_set(number, textView)
            }
            didRun = true
        }
}

private fun initAddButton(){
        // 이미 자동 생성 시작을 눌러서 번호를 추가할 수 없는 경우 고려하기
        addButton.setOnClickListener {
            if (didRun){
                Toast.makeText(this,"초기화 후에 시도해주세요. ",Toast.LENGTH_SHORT).show()
                return@setOnClickListener
            }

            if (pickNumberSet.size>=6){
                Toast.makeText(this,"번호는 6개까지만 선택할 수 있습니다. ",Toast.LENGTH_SHORT).show()
                return@setOnClickListener
            }

            if (pickNumberSet.contains(numberPicker.value)){
                Toast.makeText(this,"이미 선택한 번호입니다. ",Toast.LENGTH_SHORT).show()
                return@setOnClickListener
            }

            val textView = numberTextViewList[pickNumberSet.size]
            textView.isVisible = true
            textView.text = numberPicker.value.toString()
            
            // drawable 파일 적용하기
            number_bg_set(numberPicker.value, textView)

            pickNumberSet.add(numberPicker.value)
        }
 }
    
 private fun number_bg_set(number: Int, textView: TextView){
        // 숫자 범위에 따라 when문 적용
        when(number){
            in 1..10 -> textView.background = ContextCompat.getDrawable(this, R.drawable.circle_yello)
            in 11..20 -> textView.background = ContextCompat.getDrawable(this, R.drawable.circle_blue)
            in 21..30 -> textView.background = ContextCompat.getDrawable(this, R.drawable.circle_red)
            in 31..40 -> textView.background = ContextCompat.getDrawable(this, R.drawable.circle_gray)
            else -> textView.background = ContextCompat.getDrawable(this, R.drawable.circle_green)
        }
}
 
```  

### 3. 최종 시연  
![1](https://user-images.githubusercontent.com/59447235/147092994-d9494cc4-fcf0-4cfd-b8cf-b5adc5bf8281.jpg)
