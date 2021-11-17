### 20211117  

![버튼초기](https://user-images.githubusercontent.com/59447235/142214452-9da17700-a586-4ca6-90c6-7cd480de5936.jpg)  
위와 같은 서치뷰를 만들었다.  

menu에 있는 top_app_bar_menu에서 showAsAction부분을 ifRoom에서 ifRoom|collapseActionView로 바꿔준다.  
(collapseActionView: 사용자가 위젯과 상호작용하지 않을때 위젯을 표시하는 방법), (ifRoom: 표시할 공간이 있다면), (never: 절대로 액션바에 표시 안함)=default값  
actionViewClass를 androidx.appcompat.widget.SearchView로 설정해준다.  
![서치바메뉴](https://user-images.githubusercontent.com/59447235/142214582-cc8f2605-21a7-4753-aaf4-fc68464c767e.jpg)  



PhotoCollectionActivity에서 메뉴옵션에 대한 설정을 해준다.  
먼저, 만든 top_app_bar_menu를 inflater를 통해 연결  
서치뷰를 가져온다.  
서치뷰에 대한 설정을 apply를 통해 해준다.  
　　　　this.queryHint = "검색어를 입력해주세요"  
　　　　this.setOnQuertTextFocusChangeListener{  
　　　　　　　　서치뷰가 열림  
　　　　　　　　서치뷰가 닫힘  
　　　　}
  
에디트텍스트를 가져온다.  
에디트텍스트에 대한 설정을 apply를 통해 해준다.  
　　　　this.filters = arrayOf(InputFilter.LengthFilter(길이))  
![oncreateoptionview](https://user-images.githubusercontent.com/59447235/142219548-f293b4e2-b4d9-4cf8-8000-4c749ae699a2.jpg)  



그리고 각종 버튼에 대한 리스너들을 설정해주어 기능들을 설정해준다.  
onCreate에서 뷰와 기능을 연결해준다.  
기능들이 동작됨  
![화면 캡처 2021-11-17 232919](https://user-images.githubusercontent.com/59447235/142219910-ea0f11c7-1eab-4946-ab91-442e7d155223.jpg)  
![화면 캡처 2021-11-17 232940](https://user-images.githubusercontent.com/59447235/142219955-1faf2908-d752-46f3-941f-1604a15d6c70.jpg)  





Layout구성은 상위에 CoordinatorLayout이 있고 하위에 1.AppBarLayout 2.리사이클러뷰 3.리니어레이아웃 이 있다.  
(CoodinatorLayout: 메테리얼 디자인으로 FrameLayout에 기반을 두며, 최상위 데코뷰로 사용하거나 자식 뷰들간의 인터렉션을 위한 컨테이너로서의 사용을 주로한다.)  
(주로 '스크롤 이벤트'에 따라 '상단 앱바'의 변화를 줄때 사용한다.)  
또한 리니어레이아웃에 텍스트,스위치버튼,버튼을 포함하며 Visibility를 통해 서치뷰가 열린경우와 닫힌경우에 Visibility값을 변화해준다.  




