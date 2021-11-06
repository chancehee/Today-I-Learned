### 20211106
### 2.Android <API 튜토리얼> : 레트로핏 활용하기  

### * Retrofit: (기계 속에 원래 없던 부품 등을) 새로 장착하다 / 넣다 / 제공하다.  
### * 안드로이드에서의 Retrofit: 서버와의 HTTP통신을 통해 전달된 데이터를 앱에서 특정 형태로 받아볼 수 있게 하는 라이브러리  
　　　　　- 요약: 서버와 HTTP통신을 해서, 서버로부터 받은 데이터를 앱에서 출력해 사용자가 볼 수 있게 하는 라이브러리이다.  
　　　　　- 사용하는 이유: 서버와 클라이언트가 데이터를 주고받는 과정에서 REST API방식을 주로 사용하여 통신을 한다. 이때 AsyncTask와 HttpURLConnection을 쓰면 되지만 직접 구현해줘야 하는 것들이 꽤 많다.  
    따라서 네트워크 연결과 해제, 데이터 팡싱, 파싱된 데이터를 데이터 클래스에 저장, 에러처리 등. 이것들을 처리해주는 도구중 하나이다.  
    
### * Retrofit 기능 만들기
　　　　　- 레트로핏 클라이언트 생성: retrofitClient  
　　　　　- 레트로핏 클라이언트 가져오는 함수 : getclient(baseURL)  
　　　　　- 인터페이스 생성: IRetrofit -> searchPhotos() / searchUsers()  
　　　　　- 레트로핏 매니저 생성: val instance = RetrofitManager() / 레트로핏 인터페이스 가져오기 / API 호출하기   
　　　　　- 메인엑티비티에서 검색버튼 클릭 -> 레트로핏매니저.인스턴스.searchPhotos()  
　　　　　- 인터셉터 활용하기 : val client = OkHTTPClient.Builder() / val loggingInterceptor = HTTPLoggingInterceptor()  

