# 안드로이드 Foldable 폰 접힘 상태 확인 방법

* 1. Display Manager 를 활용한 방법

폴더블 폰은 화면을 접게 되면 바깥 디스플레이에 view 를 표시하게 됩니다.

그 때 view 는 **onResume()** 을 타게 됩니다.

onResume() 을 탈 때 display.mode 가 1인지 2인지 확인하여 접혔는지 펼친건지 상태에 따라 대응할 수 있습니다.

```kotlin
override fun onResume() {
    checkFoldedDisplay()
}

fun checkFoldedDisplay() {
    if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.P){
        val dm = applicationContext.getSystemService(Context.DISPLAY_SERVICE) as? DisplayManager
        dm?.displays?.forEach {
            
            if(it.mode.modeId == 1) {
               // mode: 1 펼친 상태

            }
            
            if(it.mode.modeId == 2) {
               // mode: 2 접힌 상태      
            }
           
        }
    }
}
```


* 2. ComponentCallbacks 의 ConfigurationChange 를 활용한 방법

시스템에서 변경 사항이 일어 날때 마다 안드로이드에서는 ComponentCallBack 을 통해서 알려주게 되는데
폴더블 폰이 접혔을 때 발생하는 디스플레이 변경 이벤트도 예외는 아닙니다.
이를 활용해서 변경이 일어났을 때 display mode 를 확인하여 대응하는 것도 하나의 방법으로 활용 할 수 있습니다.

```kotlin
private fun addComponentCallBackListener() {
    applicationContext?.registerComponentCallbacks(object : ComponentCallbacks
        override fun onConfigurationChanged(newConfig: Configuration) {
            checkFoldedDisplay()
        }

        override fun onLowMemory() {

        }
    })
}
```