# Java 와 Kotlin 에서 hilt 를 사용할 때 주의 할점

* Java만 사용할 때는 annotationprocessor 의존성을 추가한다.

* Java, Kotlin 전부 사용할 때는 Kapt 로 의존성을 추가 해야 한다.

    * Java, Kotlin 전부 사용할 때 annotationprocessor 로 의존성을 추가하면 Java 는 hilt 에서 class 를 생성하지만
     kotlin 파일에 @AndroidEntryPoint 를 해줄 시 class 를 생성못하고 build 시 에러가 발생한다.