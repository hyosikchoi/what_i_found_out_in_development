# 현재 디바이스의 언어를 가져오는 방법

* **getResources().getConfiguration()** 은 현재 앱의 리소스 구성을 가져오는 메서드입니다.
리소스 구성에는 다양한 정보가 포함되어 있습니다. 이 중에서 언어 정보를 가져오려면 **getResources().getConfiguration().locale** 를 사용해야 합니다.


```java

Locale currentLocale = getResources().getConfiguration().locale;
String language = currentLocale.getLanguage();

```

* language 변수에는 현재 디바이스의 언어 코드가 저장됩니다. 예를 들어, 한국어의 경우 "ko"가 반환될 것입니다.


* 주의: getConfiguration().locale은 오래된 API이며, **Android 7.0 (API 레벨 24)**부터는 더 이상 권장되지 않습니다. 대신 **getLocales()**를 사용하여 지원되는 모든 로케일을 가져오는 것이 좋습니다.

