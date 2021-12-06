### 20211206  

### UI
지난 번에 구현한 UI에 추가로 아래 코드를 추가해 준다.  
구분 선을 그어주기 위해 View를 사용하였고, 최근 검색어 텍스트와, 리사이클러뷰를 통해 검색어 목록을 가져오는 틀을 만들어준다.  

``` xml
        <View
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:background="@drawable/rounded_bg_gray"
            />
        <TextView
            android:id="@+id/search_history_recycler_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="최근 검색어"
            android:layout_margin="10dp"
            android:textSize="16sp"
            android:textStyle="bold"
            />
        <androidx.recyclerview.widget.RecyclerView
            android:id="@+id/search_history_recycler_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            />
```

![KakaoTalk_20211206_210915982_02](https://user-images.githubusercontent.com/59447235/144843854-59531530-a273-4e08-bbdf-aca62930b5c9.jpg)  


### 리사이클려뷰 어답터  
뷰홀더 설정시 3가지 함수 implementation (onCreateViewHolder, getItemCount, onBindViewHolder)  
조건: 1.아이템 뷰 생성  
조건: 2.뷰홀더 생성
조건: 3.인터페이스 생성
``` kotlin
class SearchHistoryRecyclerViewAdapter(searchHistoryRecyclerViewInterface: ISearchHistoryRecyclerView)
                                        : RecyclerView.Adapter<SearchItemViewHolder>() {

    private var searchHistoryList : ArrayList<SearchData> = ArrayList()

    private var iSearchHistoryRecyclerView : ISearchHistoryRecyclerView? = null

    init{
        Log.d(TAG, "SearchHistoryRecyclerViewAdapter - init() is called")
        this.iSearchHistoryRecyclerView = searchHistoryRecyclerViewInterface
    }

    // 뷰홀더가 메모리에 올라갔을때 뷰홀더와 레이아웃을 연결 시켜준다.
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): SearchItemViewHolder {
        val searchItemViewHolder = SearchItemViewHolder(
            LayoutInflater
            .from(parent.context)
            .inflate(R.layout.layout_search_item,parent,false)
            , this.iSearchHistoryRecyclerView!!
        )
        return searchItemViewHolder
    }

    override fun getItemCount(): Int {
        return searchHistoryList.size
    }

    override fun onBindViewHolder(holder: SearchItemViewHolder, position: Int) {
        val dataItem : SearchData = this.searchHistoryList[position]
        holder.bindWithView(dataItem)
    }

    // 외부에서 어답터에 데이터 배열을 넣어준다.
    // 어답터 생성시에 넣어줘도 되고 / 아래처럼 외부에서 데이터를 넣어줘도 된다. (방법은 두가지)
    fun submitList(searchHistoryList: ArrayList<SearchData>){
        this.searchHistoryList = searchHistoryList
    }
}
```


### 조건1.아이템 뷰  
``` xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="10dp"
    android:clickable="true"
    android:focusable="true"
    android:background="?attr/selectableItemBackground"
    android:id="@+id/constraint_search_item"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <TextView
        android:id="@+id/search_term_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="하하하"
        android:textSize="16sp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        />
    <TextView
        android:id="@+id/when_searched_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="2020.09.06"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintEnd_toStartOf="@id/delete_search_btn"
        android:layout_marginEnd="10dp"
        app:layout_constraintBottom_toBottomOf="parent"

        />
    <ImageView
        android:id="@+id/delete_search_btn"
        android:layout_width="30dp"
        android:layout_height="30dp"
        android:src="@drawable/ic_baseline_cancel_24"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        android:padding="5dp"
        />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### 조건2. 뷰홀더  
``` kotlin
class SearchItemViewHolder(itemView: View,
                                        searchRecyclerViewInterface: ISearchHistoryRecyclerView)
                                        : RecyclerView.ViewHolder(itemView)
                                        ,View.OnClickListener
{


    private lateinit var mySearchRecyclerViewInterface : ISearchHistoryRecyclerView
    // 뷰 가져오기
    private val searchItemTextView = itemView.search_term_text
    private val whenSearchedTextView = itemView.when_searched_text
    private val deleteSearchBtn = itemView.delete_search_btn
    private val constraintSearchItem = itemView.constraint_search_item


    init {
        Log.d(TAG, "SearchItemViewHolder - init() is called")
        // 리스너 연결
        deleteSearchBtn.setOnClickListener(this)
        constraintSearchItem.setOnClickListener(this)
        //searchItemTextView.setOnClickListener(this)
        //whenSearchedTextView.setOnClickListener(this)
        this.mySearchRecyclerViewInterface = searchRecyclerViewInterface
    }

    // 데이터와 뷰를 묶는다.
    fun bindWithView(searchItem : SearchData){
        Log.d(TAG, "SearchItemViewHolder - bindWithView() is called")
        whenSearchedTextView.text = searchItem.timestamp
        searchItemTextView.text = searchItem.term
    }

    override fun onClick(view: View?) {
        Log.d(TAG, "SearchItemViewHolder - onClick() is called")
        when(view){
            deleteSearchBtn ->{
                Log.d(TAG, "SearchItemViewHolder - 검색 삭제 버튼 클릭")
                this.mySearchRecyclerViewInterface.onSearchItemDeleteClicked(adapterPosition)
            }
            constraintSearchItem -> {
                Log.d(TAG, "SearchItemViewHolder - 검색 아이템 클릭")
                this.mySearchRecyclerViewInterface.onSearchItemClicked(adapterPosition)
            }
        }
    }
}
```

### PhotoCollectionActivity에서 사용하기  
조건: 1. 인터페이스 설정(리스너를 설정해주어서 메인 액티비티에서 알 수 있게 해준다. 2가지 implementation)  


``` kotlin
class PhotoCollectionActivity: AppCompatActivity(),
                            SearchView.OnQueryTextListener,
                            CompoundButton.OnCheckedChangeListener,
                            View.OnClickListener,
                            ISearchHistoryRecyclerView
{

    // 어답터
    private lateinit var mySearchHistoryRecyclerViewAdapter: SearchHistoryRecyclerViewAdapter
    
    // 저장된 검색 기록 가져오기 (지난 번에 구현한 내용)
    this.searchHistoryList = SharedPrefManager.getSearchHistoryList() as ArrayList<SearchData>
    
    // 검색 기록 리사이클러뷰 준비
    this.searchHistoryRecyclerViewSetting(this.searchHistoryList)

    // 검색 기록 리사이클러뷰 준비 함수
    private fun searchHistoryRecyclerViewSetting(searchHistoryList: ArrayList<SearchData>){
        Log.d(TAG, "PhotoCollectionActivity - searchHistoryRecyclerViewSetting() is called")

        this.mySearchHistoryRecyclerViewAdapter = SearchHistoryRecyclerViewAdapter(this)
        this.mySearchHistoryRecyclerViewAdapter.submitList(searchHistoryList)

        // 최근 검색어가 위로 오게하기. (뷰에 관한 설정: 최근검색어가 위로 올라오게 설정)
        val myLinearLayoutManager = LinearLayoutManager(this,LinearLayoutManager.VERTICAL,true)
        myLinearLayoutManager.stackFromEnd = true

        // apply를 통해 한번에 설정해준다.
        search_history_recycler_view.apply{
            layoutManager = myLinearLayoutManager
            this.scrollToPosition(mySearchHistoryRecyclerViewAdapter.itemCount - 1)
            adapter = mySearchHistoryRecyclerViewAdapter
        }
    }
    
    // 2가지 implementation된 함수
    // 검색 아이템 버튼 이벤트
    override fun onSearchItemClicked(position: Int) {
        Log.d(TAG, "PhotoCollectionActivity - onSearchItemClicked() is called")
        val queryString = this.searchHistoryList[position].term
        searchPhotoApiCall(queryString)
        top_app_bar.title = queryString

        this.insertSearchTermHistory(searchTerm=queryString)
        this.top_app_bar.collapseActionView()

    }

    // 검색 아이템삭제 버튼 이벤트
    override fun onSearchItemDeleteClicked(position: Int) {
        Log.d(TAG, "PhotoCollectionActivity - onSearchItemDeleteClicked() is called")
        // 해당 요소 삭제
        this.searchHistoryList.removeAt(position)
        // 데이터 덮어쓰기
        SharedPrefManager.storeSearchHistoryList(this.searchHistoryList)
        // 데이터 변경 됐다고 알려줌
        this.mySearchHistoryRecyclerViewAdapter.notifyDataSetChanged()

        handleSearchViewUi()
    }
    
    // 사진 검색 API 호출
    private fun searchPhotoApiCall(query: String){
        RetrofitManager.instance.searchPhotos(searchTerm = query,completion = {status,list ->
            when(status){
                RESPONSE_STATUS.OKAY -> {
                    Log.d(TAG, "PhotoCollectionActivity - searchPhotoApiCall() is called 응답 성공 / list.size: ${list?.size}")

                    if (list != null){
                        this.photoList.clear()
                        this.photoList = list
                        this.photoGridRecyclerViewAdapter.submitList(this.photoList)
                        this.photoGridRecyclerViewAdapter.notifyDataSetChanged()
                    }
                }
                RESPONSE_STATUS.NO_CONTENT ->{
                    Toast.makeText(this,"$query 에 대한 검색 결과가 없습니다.",Toast.LENGTH_SHORT).show()
                }
            }
        })
    }
    
    override fun onClick(view: View?) {
        when(view){
            clear_search_history_button ->{
                Log.d(TAG, "검색 기록 삭제 버튼이 클릭 되었다.")
                SharedPrefManager.clearSearchHistoryList()
                this.searchHistoryList.clear()
                // ui 처리
                handleSearchViewUi()
            }
        }
    }
    
    private fun handleSearchViewUi(){
        Log.d(TAG, "PhotoCollectionActivity - handleSearchViewUi() is called / size : ${this.searchHistoryList.size}")

        if(this.searchHistoryList.size > 0){
            search_history_recycler_view.visibility = View.VISIBLE
            search_history_recycler_label.visibility = View.VISIBLE
            clear_search_history_button.visibility = View.VISIBLE

        }else{
            search_history_recycler_view.visibility = View.INVISIBLE
            search_history_recycler_label.visibility = View.INVISIBLE
            clear_search_history_button.visibility = View.INVISIBLE
        }
    }
    
}
```
### SharedPrefManager 에서 추가적인 기능 구현  
``` kotlin
// 검색 목록 가져오기
    fun getSearchHistoryList() : MutableList<SearchData>{


        // 쉐어드 가져오기
        val shared = App.instance.getSharedPreferences(SHARED_SEARCH_HISTORY, Context.MODE_PRIVATE)

        val storedSearchHistoryListString = shared.getString(KEY_SEARCH_HISTORY, "")!!

        var storedSearchHistoryList = ArrayList<SearchData>()

        // 검색 목록이 값이 있다면
        if (storedSearchHistoryListString.isNotEmpty()){
            // 저장된 문자열을 -> 객체 배열로 변경
            storedSearchHistoryList = Gson().fromJson(storedSearchHistoryListString, Array<SearchData>::class.java).toMutableList() as ArrayList<SearchData>
        }

        return storedSearchHistoryList
    }

    // 검색 목록 지우기
    fun clearSearchHistoryList(){
        Log.d(TAG, "SharedPrefManager - clearSearchHistoryList() is called")

        // 쉐어드 가져오기
        val shared = App.instance.getSharedPreferences(SHARED_SEARCH_HISTORY, Context.MODE_PRIVATE)

        // 쉐어드 에디터 가져오기
        val editor = shared.edit()

        // 해당 데이터 지우기
        editor.clear()

        // 변경 사항 적용
        editor.apply()

    }
```


### 인터페이스  
``` kotlin
interface ISearchHistoryRecyclerView {

    // 검색 아이템 삭제 버튼 클릭
    fun onSearchItemDeleteClicked(position : Int)

    // 검색 버튼 클릭
    fun onSearchItemClicked(position: Int)

}
```





