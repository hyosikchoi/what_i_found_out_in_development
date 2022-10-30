# 안드로이드 4대컴포넌트 하나중 Service에서 startService 와 bindService 는 같은 **Service** 에서 사용이 가능하다.

* 같은 Service 에서 startService를 호출 시 **onStartCommand** 메서드가 실행되고 bindService 호출 시 **onBind** 메서드가 실행된다.

* [startService,bindService lifecycle 관련 참조](https://stackoverflow.com/questions/3514287/android-service-startservice-and-bindservice)

# Task Manager 에서 앱을 강제로 kill process 할 시 startService 에서만 감지가 가능하다.

* startService 로 실행하게 되면 앱을 강제로 kill 할 시 **onTaskRemoved** 메서드가 호출 된다.


# 오레오(26) 버전 이상부턴 startService 가 아닌 **startForegroundService** 를 사용해야 한다.

* 여기서 startForegroundService 는 **5초 안에 Service객체 안에서 startForeground() 를 호출해야 한다.**
* 그렇지 않으면 **ANR** 이 발생합니다.

# startForegroundService 사용 시 android 12(31)이상 Notification 10초 딜레이 후 생성 관련

```java
new NotificationCompat.Builder(...)
                .setForegroundServiceBehavior(NotificationCompat.FOREGROUND_SERVICE_IMMEDIATE)
```

* 서비스는 알림을 설정할 때 FOREGROUND_SERVICE_IMMEDIATE를 setForegroundServiceBehavior()에 전달하여 동작 변경을 선택 해제

* [startForegroundService Notification 10초 딜레이 관련 참조](https://stackoverflow.com/questions/73074639/android-foreground-service-notification-delayed)
