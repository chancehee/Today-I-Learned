### 20211216  

### BMI 어플: 다음페이지에 변수 넘겨주기, 넘겨준 변수로 BMI 계산하여 UI에 출력하기  

### 메인 액티비티: 변수 넘겨주기(putExtra(name,value))  
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 컴퓨터에게 어떤 타입인지 알려주는 방법 2가지 (명시적/추론적)
        val heightEditText: EditText = findViewById(R.id.heightEditText)
        val weightEditText = findViewById<EditText>(R.id.weightEditText)

        val resultButton = findViewById<Button>(R.id.resultButton)

        resultButton.setOnClickListener {
            Log.d(TAG, "MainActivity - ResultButton 이 클리되었습니다.")

            if (heightEditText.text.isEmpty() || weightEditText.text.isEmpty() ){
                Toast.makeText(this,"빈 값이 있습니다.",Toast.LENGTH_SHORT).show()

                // setOnClickListener 함수를 나간다
                return@setOnClickListener

            }
            val height : Int= heightEditText.text.toString().toInt()
            val weight : Int= weightEditText.text.toString().toInt()

            val intent = Intent(this, ResultActivity::class.java)
            
            // 인텐트에 (name,value) 형태로 데이터를 담아준다.
            intent.putExtra("height",height)
            intent.putExtra("weight",weight)
            startActivity(intent)

        }
    }
}
```

### 두번째 액티비티(ResultActivity): 인텐트에서 값을 가져와서 bmi 계산 수행  
```kotlin
class ResultActivity : AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_result)

        // 넘겨준 데이터 형태가 Int 형태 이므로 getIntExtra 함수 사용
        // getIntExtra(받아올값 name, 디폴트 값)
        val height = intent.getIntExtra("height", 0)
        val weight = intent.getIntExtra("weight", 0)

        // Math.pow 형태로 사용도 가능하지만 double 형에서 바로 pow 함수가 사용가능하므로 바로 사용
        val bmi = weight / (height / 100.0).pow(2.0)

        val bmiNumber = findViewById<TextView>(R.id.bmi_result_number)
        val bmitxt = findViewById<TextView>(R.id.bmi_result_text)

        val resultText = when {
            bmi >= 35.0 -> "고도 비만"
            bmi >= 30.0 -> "중정도 비만"
            bmi >= 25.0 -> "경도 비만"
            bmi >= 23.0 -> "과체중"
            bmi >= 18.5 -> "정상체중"
            else -> "저체중"
        }

        bmiNumber.text = bmi.toString()
        bmitxt.text = resultText
    }
}
```

### activity_result.xml : bmi 결과 값과 비만도 정도를 텍스트뷰에 보여준다.  
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="vertical"
    android:gravity="center">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">
        <TextView

            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="BMI: "
            android:textSize="20dp"/>
        <TextView
            android:id="@+id/bmi_result_number"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="20dp"
            tools:text = "233.33"
            />

    </LinearLayout>

    <LinearLayout
        android:layout_marginTop="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="비만도: "
            android:textSize="20dp"
            />
        <TextView
            android:id="@+id/bmi_result_text"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="보통"
            android:textSize="20dp"
            />
    </LinearLayout>

</LinearLayout>
```
### 최종 결과: BMI 어플 마무리  
![1](https://user-images.githubusercontent.com/59447235/146302088-cbc41a83-e008-4a8e-8708-d7104261f2f6.jpg)![2](https://user-images.githubusercontent.com/59447235/146302096-04053d48-ff38-4b0e-b6da-a419b47550f6.jpg)


-------------------------------------------------------------------------------------------------------------------------------  

### 인텐트 공부  
  인텐트란 메시징 객체로, 다른 앱 구성 요소로부터 작업을 요청하는데 사용할 수 있다.  
  인텐트는 시작할 액티비티를 설명하고 모든 필수 데이터를 담는다.  
![intent-filters_2x](https://user-images.githubusercontent.com/59447235/146301161-6ffeb12c-35be-486f-b1e0-803c5a96761e.png)   
출처: https://developer.android.com/guide/components/intents-filters?hl=ko (안드로이드 공식 문서)  
  1번에서 인텐트에 데이터를 담고 3번에서 인텐트에 담긴 데이터를 받아서 사용한다.  
  2번에서는 메니페스트에 안드로이드 운영체제에게 새로 생긴 액티비티가 있다거나 이러한 정보를 알려줘야 한다.
