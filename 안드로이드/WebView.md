# WebView란?

* WebView는 웹 콘텐츠를 표시하는 데 사용되는 컴포넌트이다.

# WebViewClient란?

* WebViewClient는 안드로이드의 WebView에서 **웹 페이지 로딩 및 관련 이벤트를 처리하기 위한** 클래스입니다. 

# WebViewClient 사용시 주의할 점

* WebViewClient의 **shouldOverrideUrlLoading()** 메소드는 특정 URL이 로딩될 때 호출되는데, 이 때 WebView의 기본 동작을 대체할 수 있습니다. 예를 들어, 특정 URL에 대해 앱 내부에서 처리할 로직을 구현하거나, 외부 브라우저로 URL을 열도록 지정할 수 있습니다.

그러나 WebViewClient의 shouldOverrideUrlLoading() 메소드를 오버라이드할 때, 주의할 점이 있습니다. WebViewClient를 설정하면 WebView의 요청을 다루기 위해 Android 시스템의 ApplicationContext가 사용될 수 있습니다. 이로 인해 **ApplicationContext가 재구성**될 수 있으며, 이는 액티비티가 재생성되는 것과 유사한 동작을 보일 수 있습니다.

따라서, WebViewClient를 사용할 때에는 **ApplicationContext가 재구성될 수 있다는 점을 염두에 두고 작업을 수행해야 합니다.** 예를 들어, **ApplicationContext에 의존하는 작업이 있다면 이를 고려하여 적절한 처리를 해주어야 합니다.** 또한, WebView를 사용하는 액티비티의 라이프사이클 변화에 대한 올바른 처리도 중요합니다.