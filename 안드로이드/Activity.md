# **savedInstanceState**를 이용하여 Bundle에 값을 저장 했다가 사용하는 방법

```kotlin
override fun onPause() {
        super.onPause()
        Log.d("saveInstance" , "onPause")
    }

override fun onSaveInstanceState(outState: Bundle) {
        super.onSaveInstanceState(outState)
        outState.putInt("save" , 24)
        Log.d("saveInstance" , "저장")
    }
```

* onSaveInstanceState 메서드에서 Bundle에 값을 먼저 저장하게끔 해야 합니다.
* Activity의 Lifecycle이 onPause 된 후에 onSaveInstanceState를 호출하여 값을 저장하게 됩니다.


```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        if(savedInstanceState != null) {
            val saveInt = savedInstanceState.getInt("save")
            Log.d("saveInstance" , "저장 된 값 : $saveInt")
        }
        Log.d("saveInstance" , "onCreate")
}        
```

* 그 후에 화면회전등 다시 한번 onCreate가 호출될 때 savedInstanceState Bundle에 값이 저장 되있다면 값을 불러오게 됩니다.

* Ex) 화면 회전을 통해 찍은 로그값

```
2023-02-06 00:54:17.300 4788-4788/com.hyosik.android.diary D/saveInstance: onPause
2023-02-06 00:54:17.306 4788-4788/com.hyosik.android.diary D/saveInstance: 저장
2023-02-06 00:54:17.340 4788-4788/com.hyosik.android.diary D/saveInstance: 저장 된 값 : 24
2023-02-06 00:54:17.340 4788-4788/com.hyosik.android.diary D/saveInstance: onCreate
```
