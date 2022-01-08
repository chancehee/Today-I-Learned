### 20220109  

## 구현할 기능: 1. ImageView UI구현 2. SAF 기능을 활용하여 로컬파일 열어주기   

### 1.ImageView UI구현  
- 리니어 레이아웃 2개를 통해 이미지뷰 3개씩 2번 총 6개 구현  
- constraintDimensionRatio를 통해 종횡비율을 설정해준다. (w, 1:3 뜻 H를 먼저 할당해주고 1:3의 비율로 W를 할당해준다는 뜻)
- scaleType을 centercrop으로 설정해주어서 이미지의 잘린 부분은 무시하고 크기가 일정하게 해준다.
```xml
<LinearLayout
        android:id="@+id/firstRowLinearLayout"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintDimensionRatio="W, 1:3"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        >
        <ImageView
            android:id="@+id/imageView11"
            android:scaleType="centerCrop"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="match_parent"/>
        <ImageView
            android:id="@+id/imageView12"
            android:scaleType="centerCrop"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="match_parent"/>
        <ImageView
            android:id="@+id/imageView13"
            android:scaleType="centerCrop"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="match_parent"/>
    </LinearLayout>

    <LinearLayout
        android:id="@+id/secondtRowLinearLayout"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintDimensionRatio="H, 3:1"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/firstRowLinearLayout"
        >
        <ImageView
            android:id="@+id/imageView21"
            android:scaleType="centerCrop"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="match_parent"/>
        <ImageView
            android:id="@+id/imageView22"
            android:scaleType="centerCrop"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="match_parent"/>
        <ImageView
            android:id="@+id/imageView23"
            android:scaleType="centerCrop"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="match_parent"/>
    </LinearLayout>
```  

### 2. SAF 기능을 활용하여 로컬파일 열어주기  
- ImageViewList에 6개의 이미지를 추가  
```kotlin
// mutable리스트에 이미지 뷰를 추가해주는 방법 / 아니면 초기에 이미지 6개를 리스트에 담아놓고 할당하는 방식 두가지 다 가능한 듯
    private val ImageViewList : List<ImageView> by lazy{
        mutableListOf<ImageView>().apply {
            add(findViewById(R.id.imageView11))
            add(findViewById(R.id.imageView12))
            add(findViewById(R.id.imageView13))
            add(findViewById(R.id.imageView21))
            add(findViewById(R.id.imageView22))
            add(findViewById(R.id.imageView23))
        }
    }
```
- 권한을 승인하였는지 거절하였는지 확인하는 함수(현재): onRequestPermissionResult()를 통해서 확인 / (권한이 이미 있는 경우와는 다르다.)(=과거)
```kotlin
override fun onRequestPermissionsResult(
        requestCode: Int,
        permissions: Array<out String>,
        grantResults: IntArray
    ) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults)

        when(requestCode){
            1000 -> {
                // 권한이 부여될 때 바로 사진탐색하는 함수 실행
                if (grantResults.isNotEmpty() && grantResults[0] == PackageManager.PERMISSION_GRANTED){
                    // todo 권한이 부여된 것입니다.
                    navigatePhotos()
                }
                else{
                    Toast.makeText(this,"권한을 거부하셨습니다.",Toast.LENGTH_SHORT).show()
                }
            }
            else -> {
                //
            }
        }
    }
```
- SAF(Storage Access Framework)를 통해서 사진을 읽어오기 (intent를 설정해주어 실행시켜준다.)
- startActivityForResult()가 deprecated 되어서 -> ActivityResultLauncher<Intent> 타입의 변수.launch(intent)를 통해 대체기능함수를 찾았다. (requestCode 불필요하다.)
- 또한 registerForActivityResult(ActivityResultContracts.StartActivityForResult()를 통해서 일종의 계약(?)을 정한 후 사용한다.
```kotlin

private lateinit var getResult: ActivityResultLauncher<Intent>
  
getResult = registerForActivityResult(ActivityResultContracts.StartActivityForResult()){}
  
private fun navigatePhotos() {
        // SAF기능을 실행하여 Content를 가져오는 기능
        val intent = Intent(Intent.ACTION_GET_CONTENT)
        intent.type = "image/*"

        //startActivityForResult(intent, 2000) -> deprecated 됨
        getResult.launch(intent)
    }
```
  
### 화면  
![1](https://user-images.githubusercontent.com/59447235/148650763-cd80beea-c49f-42bc-8c8b-9e059b3e5d40.jpg)![2](https://user-images.githubusercontent.com/59447235/148650766-d9907b02-41f4-49c8-a270-e5770d85a6a1.jpg)









