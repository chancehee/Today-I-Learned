### 20211123  

### 쉐어드 로컬 저장1: 검색어 / 검색시간을 검색버튼을 누를때 쉐어드로컬에 저장하고 불러오는 기능 구현  
  
  
#### 1. 데이터 클래스: 검색어 / 검색시간을 다룰 데이터 형태이다.  
`data class SearchData(val timestamp, val term){}`

#### 2. 데이터클래스 가져오기 / 데이터클래스 저장하기 함수를 갖는 클래스.  
``` kotlin
object SharedPrefManager{
  private const val Locker = ""
  private const val KEY = ""
  
  // 1) 데이터클래스 저장하기  
  fun storeSearchHistoryList(searchHistoryList: MutableList<SearchData>){
    // 매개변수로 들어온 배열을 문자열로 변환
    val searchHistoryList_String : String = Gson().toJson(searchHistoryList)
    
    // 쉐어드 가져오기(사물함)
    val shared = App.instance(context).getSharedPreferences(Locker, Context.MODE_PRIVATE)
    
    // 쉐어드 에디터 가져오기
    val editor = shared.edit()
    // shared 사물함의 이름이 Locker에 KEY를 통해 문자열 저장
    editor.putString(KEY, searchHistoryList_String)
    editor.apply()
  }
  
  // 2) 데이터클래스 가져오기
  fun getSearchHistoryList() : MutableList<SearchData>{
    // 쉐어드 가져오기
    val shared = App.instance.getSharedPreferences(Locker, Context.MODE_PRIVATE)
    
    // 열쇠인 KEY를 통해 shared 사물함 Locker에 저장된 값을 가져온다 / 없을경우 빈문자열가져오기
    val storedSearchHistoryList_String = shared.getString(KEY, "")!!  // 값이 무조건 존재한다.
    
    var storedSearchHistoryList = ArrayList<SearchData>()
    
    if (storedSearchHistoryList_String.isNotEmpty()){
      // 저장된 문자열을 객체 배열로 변환
      storedSearchHistoryList = Gson().fromJson(storedSearchHistoryList_String, Array<SearchData>::class.java).toMutableList() as ArrayList<SearchData>
    } 
    return storedSearchHistoryList
  }
  
}
```

#### 3. 액티비티에서 기능 테스트 : 위에서 구현한 함수를 액티비티에서 활용하기  
``` kotlin

// 검색기록을 저장하기 위한 리스트 선언
private var searchHistoryList = ArrayList<SearchData>()

// 검색버튼이 클릭되었을때
val newSearchData = SearchData(term = query, timestamp = Date()) // 검색어와 검색시간을 담을 데이터클래스 선언
this.searchHistoryList.add(newSearchData) // 검색기록을 저장하기 위한 리스트에 add한다.
SharedPrefManager.storeSearchHistoryList(this.searchHistoryList) // 쉐어드에 저장한다.

// oncreate 되었을때 검색기록 가져오기
this.searchHistoryList = SharedPrefManager.getSearchHistoryList() as ArrayList<SearchData> // 가져온 Mutable형태를 ArrayList형태로 받는다.
```

### 느낀점: 안드로이드에 DB없이 간단하게 저장하는 쉐어드 로컬 기능에 대해서 알았고, 이를 통해 검색기록을 저장하고 불러 올 수 있으며 사물함/열쇠 형태로 작동하고 Gson을 활용하여 데이터의 형변환이 이루어지는것을 배웠다. 



