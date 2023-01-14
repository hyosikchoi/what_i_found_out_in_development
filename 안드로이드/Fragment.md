# Fragment 의 show , hide 상태 체크하기

* onHiddenChanged() 함수에서 상태 체크가 가능하다.

```kotlin
// Fragment 상태(show, hide)가 변경될 때마다 호출
override fun onHiddenChanged(hidden: Boolean) {
    super.onHiddenChanged(hidden)

    if (hidden) { // hide일 때
        
    } else { // show일 때
        
    }
}
```