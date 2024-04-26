# collectAsState() 란?

* Flow나 StateFlow와 함께 사용됩니다. 이 함수는 Flow나 StateFlow의 최신 값을 관찰하고, 값이 업데이트될 때마다 Compose UI를 다시 그리도록 합니다.

# collcectAsState vs collectAsStateWithLifecycle

* collectAsState 는 앱이 백그라운드로 진입해도 계속해서 flow 로부터 데이터를 collect 하고 있습니다. 
* 반대로 collectAsStateWithLifecycle 는 앱이 **onStop** 에 진입 하고 **onStart** 가 되기 전까지 flow 로부터 데이터를 collect 하지 않습니다.