### 20211215  

### BMI 어플 : 변수 설정 및 인텐트 이동  
에딧 텍스트에서 입력한 값을 변수로 받아오는 방법과 버튼을 눌렀을 때 인텐트 이동하는 방법을 공부했다.  

### 메인 액티비티: 변수로 받아오기  
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        // xml 파일에서 컴포넌트를 가져오기
        // 컴퓨터에게 어떤 타입인지 알려주는 방법 2가지 (명시적/추론적)
        val heightEditText : EditText = findViewById(R.id.heightEditText) //명시적
        val weightEditText = findViewById<EditText>(R.id.weightEditText) //추론적
        val resultButton = findViewById<Button>(R.id.resultButton) //추론적
        
        // 버튼에 리스너 달아주기 
        resultButton.setOnClickListener{
            // 두가지 에딧 텍스트중 하나라도 빈 값이 있다면 
            if (heightEditText.text.isEmpty() || weightEditText.text.isEmpty()){
                // 토스트 메시지 띄우기 
                Toast.makeText(this, "빈 값이 있습니다.", Toast.LENGTH_SHORT).show()
                
                // setOnClickListener 함수를 나간다.
                return@setOnClickListener
            }
            
            // 입력된 값을 변수에 저장하기
            val height : Int = heightEditText.text.toString().toInt()
            val weight : Int = weightEditText.text.toString().toInt()
            
            // * 실행하기 전에 액티비티가 있다라는 것을 메니페스트에 등록시켜 컴퓨터에게 알려주어야 한다. *
            // 인텐트 생성하기 (이전 액티비티=this, 이동할 액티비티::class.java)
            val intent = Intent(this, ResultActivity::class.java)
            // 인텐트 실행하기
            startActivity(intent)
        }
    }
}
        
```

### 두번째 액티비티(ResultActivity) : xml 파일을 onCreate()시에 연결시켜주기
```kotlin
class ResultActivity : AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // xml 과 activity 연결 해주기
        setContentView(R.layout.activity_result)
    }
}
```

### 메니페스트에 등록하기(액티비티를 생성하면 컴퓨터가 모르기 때문에 메니페스트에서 알려준다.)  
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.chancehee.aop_part2_chapter01">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Aoppart2chapter01">
      
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
      
        <activity android:name=".ResultActivity"/>
    </application>

</manifest>
```

### xml 파일 생성 (activity_result.xml)  
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

</androidx.constraintlayout.widget.ConstraintLayout>
```  


![1](https://user-images.githubusercontent.com/59447235/146178566-634fc054-1599-4f39-b88c-d333916a5f7f.jpg)![2](https://user-images.githubusercontent.com/59447235/146178620-20613379-1b1d-4ddc-a45b-6ed93b2e65d6.jpg)![3](https://user-images.githubusercontent.com/59447235/146178652-300ca1e2-44bb-4c8c-ab16-0ce2970d83cb.jpg)
