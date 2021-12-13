### 20211214  

### BMI 어플 UI 구현  
LinearLayout, TextView, EditText, Buttom 을 사용하여 구현 하였고, padding 과 margin의 차이점을 공부하였다.  

margin: 어떤 컴포넌트 밖에 공간(여백)을 채우는 것  
padding: 어떤 컴포넌트 안에 공간(여백)을 채우는 것  

``` xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:textColor="@color/custom_black"
        android:textStyle="bold"
        android:textSize="20sp"
        android:text="@string/height"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:layout_marginTop="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:inputType="number"/>

    <TextView
        android:textColor="@color/custom_black"
        android:textStyle="bold"
        android:textSize="20sp"
        android:layout_marginTop="30dp"
        android:text="@string/weight"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:layout_marginTop="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:inputType="number"/>

    <Button
        android:layout_marginTop="50dp"
        android:text="확인하기"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
</LinearLayout>
```

custom_black은 기존 black(#000000) 컬러가 너무 진한 검정이라 연한 검정으로 지정해 주었다.
```xml
<resources>
    <color name="custom_black">#222222</color>
</resources>
```

체중과 신장은 string.xml 파일에 지정해 주어 사용하였다.
```xml
<resources>
    <string name="weight">체중</string>
    <string name="height">신장</string>
</resources>
```

![KakaoTalk_20211214_004627005](https://user-images.githubusercontent.com/59447235/145845384-c975c3d6-ca3a-4dae-a98c-63825f6cb6fc.jpg)![KakaoTalk_20211214_004633807](https://user-images.githubusercontent.com/59447235/145845481-f7dba530-aaf1-45fc-884f-9f6d1190df0f.jpg)  
EditText에서 inputType을 number로 지정해주었다.

