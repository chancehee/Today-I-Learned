### 20220211  

## 구현할 기능: 1. editText에 입력한 주소창을 웹뷰에 띄워주기  

### 1. editText에 입력한 주소창을 웹뷰에 띄워주기  
- editText의 inputType을 textUri로 설정하여, 입력할 때 키보드를 uri 관련 키보드로 띄워준다.
- imeOption을 actionDone으로 설정하여, 키보드의 모서리 버튼 UI를 지정 해준 작업 값에 따라서 설정해준다.  
(액션버튼을 조금 더 명시하기 위해서 사용한다.)
- 설정한 버튼을 클릭 하였을 때, setOnEditorActionListener() 라이브러리를 사용하여 기능을 구현해준다.  
(Action 버튼을 눌렀을 때 알 수 있도록, 리스너를 세팅해주는 메소드가 setOnEditorActionListener() 이며, imeOption = ActionId 이다.)  
(리스너를 통해 작업 버튼 누르기를 수신 대기할 수 있다. 리스너에서는 IME_ACTION_SEND와 같은 EditorInfo 클래스에 정의된 적절한 IME 작업 ID에 응답한다.  

```xml
<EditText
      android:imeOptions="actionDne"
      android:inputType="textUri"
      />
```  

```kotlin
class MainActivity : AppCompatActivity() {
    private val webView : WebView by lazy{
        findViewById(R.id.webView)
    }

    private val addressBar : EditText by lazy{
        findViewById(R.id.addressBar)
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        initViews()
        bindViews()
    }

    // 명시된 url을 불러오는 작업
    @SuppressLint("SetJavaScriptEnabled")
    private fun initViews(){
        // apply람다식 함수를 사용하여 내부에서 this로 작동하여 가독성이 좋게 설정을 해준다.
        webView.apply{
            webViewClient = WebViewClient()
            settings.javaScriptEnabled = true
            loadUrl("http://www.google.com")
        }
    }

    // xml파일에서 설정해준 imeOption설정을 actionId로 받아와서 확인 후, editText에 입력한 문자열 값을 로드해준다.
    // setOnEditorActionListener() 함수는 3개의 파라미터 값을 갖는다. 1.view 2.actionId 3.event 이를 통해서 true 아니면 false 값을 반환한다.
    private fun bindViews() {
        addressBar.setOnEditorActionListener{ v,actionId,event ->
            if (actionId == EditorInfo.IME_ACTION_DONE){
                webView.loadUrl(v.text.toString())
            }
            // editText에서 완료를 한 후에 텍스트를 내려주기 위하여 false로 지정해준다. (true/false 는 해당 작업을 다 consume 하였는지 아닌지 판단해준다.)
            return@setOnEditorActionListener false
        }
    }
}
```  

### 화면
![2](https://user-images.githubusercontent.com/59447235/153613239-05491629-ce8e-4954-869d-b2490ba059ae.jpg)![1](https://user-images.githubusercontent.com/59447235/153612919-93d1a00b-4124-4431-acc2-204aa9ff65c1.jpg)  

### editText에서 권장하는 방식  
- input type 지정  
ex) phone, textPassword, password, textAutoCorret 등  
- 입력 방법 작업 지정  
대부분의 소프트 입력 방법에서는 현재 텍스트 필드에 적합한 사용자 작업 버튼을 하단 모서리에 제공한다.  
기본적으로 시스템은 이 버튼을 다음 작업 또는 완료 작업에 사용한다.  
단, 여러 줄 텍스트를 허용하는 경우는 예외  
ex) actionSend, actionSearch, actionDone 등  
- 자동 완성 제안 제공 기능






