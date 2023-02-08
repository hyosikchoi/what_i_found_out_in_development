* Annotation 이란 **주석**이라는 의미를 가지고 있는 녀석이다.

특정 클래스 , 변수 , 메소드 등에 붙이는 코드로 해당 타겟의 기능을 좀더 **명확**하게 해주는 역할을 한다.


하지만 이런 어노테이션에서 동작하는 방식은 크게 2가지로 나뉩니다.

1. java.lang.reflection 을 이용해서 Class 정보를 읽어 Instance 의 타겟에 Annotation 에 해당되는 기능을 정의하는 방식 **(리플렉션이란 객체를 통해 클래스의 정보를 분석해 내는 프로그램 기법을 말한다. 투영, 반사 라는 사전적인 의미를 지니고 있다)**
[reflection 설명 참조](https://gyrfalcon.tistory.com/entry/Java-Reflection)

2. Annotation Processing Tool(APT) 을 이용하여 Compile 단계에서 Annotation 이 정의된 타겟의 정보를 미리 정의하는 방식


위의 2가지 방식 중에서는 2의 방식이 성능면에서 좋은 방식입니다. 하지만 APT 에 의한 방식은 Compile 된 클래스가 A.class -> A_.class 라는 식으로 “_” 가 붙는 단점이 있습니다.

* java.lang.reflection? Annotation Processing Tool?
Reflection 을 활용한 방법은 APT 에 대한 학습에 비하면 다소 쉬운면이 있습니다. 하지만 **Runtime** 시에 annotation 분석을 하기 때문에 **성능상 이슈**가 있습니다. 반면 APT 를 활용한 방식은 **컴파일시 시간적인 비용**과 APT 를 통해 생성된 코드는 **A.java -> A_.java 와 같은 형태로 변한다는 단점**이 있으나 **Runtime 시 성능상 이점**이 있습니다.


* AndroidAnnotations, ButterKnife, Dagger 등이 APT 를 이용하여 안드로이드를 지원하고 있습니다.