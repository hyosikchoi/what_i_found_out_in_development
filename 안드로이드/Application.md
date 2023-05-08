# Application 에서 Activity의 활동을 추적하는 방법

*  **registerActivityLifecycleCallbacks** 을 등록해서 로그를 출력할 수 있습니다.

```kotlin

class App : Application() {
  override fun onCreate() {
    ...
    registerActivityLifecycleCallbacks(object : ActivityLifecycleCallbacks {
      // Logging
    })
  }
}

```

혹은 braze 와 같은 sdk 를 사용시

**registerActivityLifecycleCallbacks(BrazeActivityLifecycleCallbackListener())**

위와 같이 사용할 수도 있습니다.