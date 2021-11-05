### 1.Android <API 튜토리얼> 레이아웃 설정 : 메테리얼 테마를 활용하여 전체적인 UI를 구성하기

### * 메테리얼 테마
  - 정의: 인터페이스의 구성요소들의 "기본 속성들" 을 미리 만들어 놓은 도구.
  - 장점: 리소스와 기능이 포함된 컴포넌트를 커스텀하지 않고 기본 테마 그대로 사용하면 커뮤니케이션 비용이 줄어들고 오류가 일어날 확률도 적어진다.

### * 레이아웃 제작
  - 구성:   
　　1. activity_main.xml :  ScrollView / LinearLayout / ImageView: 'Unsplash아이콘'(벡터에셋) / RadioGroup(radiobutton) /  
　　　　　material.TextInputLayout -> material.TextInputEditText / custombutton  
　　2. custombutton : FrameLayout / MaterialButton / ProgressBar
  - 겪은 문제: 커스텀버튼을 생성할 때, MaterialButton에 ProgressBar을 올려놓고 visible 과 invisible 을 통하여 컨트롤 하려 하였으나 버튼이 레이아웃에 1순위로 보이는 성질 때문에
               ProgressBar에 elevation(고도) = 7dp 로 설정하여 해결하였다. ( elevation은 해당 View를 Z축으로 이동하여 그림자를 컨트롤하게 해주는 메테리얼 디자인이다.) 
### * 기능 제작
1.main activity  
　　　　　oncreate  
　　　　　라디오그룹.setOnCheckedChangeListener{그룹, 선택된 아이디 ->  
　　　　　　　　　　when(선택된 아이디){  
　　　　　　　　　　　　　　　사진버튼 -> UI변경   
　　　　　　　　　　　　　　　사용자버튼 -> UI변경  
　　　　　　　　　　　　　　　}  
　　　　　}  
　　　　　search_term_edit_text.addTextChangedListener(object : TextWatcher{  
　　　　　　　　　　1.텍스트가 바뀐 후  
　　　　　　　　　　2.텍스트가 바뀌기 전  
　　　　　　　　　　3.텍스트가 변경될 때(글자가 입력되면 버튼 visible / 글자가 없으면 버튼 invisible / 글자 maxlength 설정)    
 　　　　　}  
　　　　　검색버튼.setOnClickListener{  
　　　　　　　　　　this.handleSearchButtonUi(){  
　　　　　} // oncreate  
     
　　　　　private finhandleSearchButtonUi(){  
　　　　　　　　　　// 버튼이 눌린경우에 '버튼' 글자는 " ", 'ProgressBar'는 visible  
　　　　　　　　　　Handler().postDelayed({  
　　　　　　　　　　　　　　　// 'ProgressBar' = invisible  
　　　　　　　　　　　　　　　// '버튼' = '검색'  
　　　　　　　　　　}, 1500)  
　　　　　}  
  - 겪은 문제2: Handler().postDelayed 부분이 곧 사라진다고 한다. 따라서 Handler(Looper.getMainLooper()).postDelayed사용  
  

          
  
  

### * UI
![KakaoTalk_20211105_141550895](https://user-images.githubusercontent.com/59447235/140462356-3a69ec25-1530-476b-93e1-7279913f500f.jpg)

