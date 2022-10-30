# 안드로이드 4대컴포넌트 하나중 Service에서 startService 와 bindService 는 같은 **Service** 에서 사용이 가능하다.

* 같은 Service 에서 startService를 호출 시 **onStartCommand** 메서드가 실행되고 bindService 호출 시 **onBind** 메서드가 실행된다.


# Task Manager 에서 앱을 강제로 kill process 할 시 startService 에서만 감지가 가능하다.

* startService 로 실행하게 되면 앱을 강제로 kill 할 시 **onTaskRemoved** 메서드가 호출 된다.