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


# Fragment 'Could not find Fragment constructor' 에러 관련 

* 해당 에러는 RuntimeException 중 하나로, 주로 Fragment를 생성할 때 **생성자 매개변수**를 넣어서 만들었기 때문에 발생합니다.

* 안드로이드 시스템상 **메모리 부족, 화면 회전으로 인한 재구성(onConfigurationChanged 메서드 구현 x 경우)** Fragment 를 파괴했다가 재구성하는 경우가 생기게 된다.

이 때, Fragment **instantiate** 메서드를 통해 재구성을 하는데 이 때 사용하는 생성자가 **기본 생성자를 이용하게 된다.**

그래서 기본 생성자가 정의되어 있지 않으면 해당 에러가 발생하게 됩니다.


* **처리 방법**

1. FragmentFactory 이용

* FragmentFactory 를 하나 생성해서 instantiate 메서드를 override 하여 생성자 매개변수를 넣어서 생성하는 구조로 바꿔줍니다. 

```kotlin

class MyFragmentFactory(private val index: Int): FragmentFactory() {

    override fun instantiate(classLoader: ClassLoader, className: String): Fragment {
        return when (className) {
            MyFragment::class.java.name -> MyFragment(index)
            else -> super.instantiate(classLoader, className)
        }
    }
}

```

* 그리고나서 fragmentManager 의 factory 에 해당 factory 를 설정 해줍니다.

```kotlin

  override fun onCreate(savedInstanceState: Bundle?) {
        supportFragmentManager.fragmentFactory = MyFragmentFactory()
        super.onCreate(savedInstanceState)
        binding = DataBindingUtil.setContentView(this, layoutId)
        
        val fragment = supportFragmentManager.fragmentFactory.instantiate(classLoader, MyFragment::class.java.name)
        supportFragmentManager.commit {
            add(containerId, fragment, MyFragment.TAG)
            addToBackStack(null)
        }
    }

```


2. Fragment Arguments 이용

* 어떻게 보면 가장 간단한 방법이다. fragment 생성시 **Bundle** 객체에 담아서 fragment 라이프싸이클 시작 지점에서 Bundle 에서 꺼내와서 값을 세팅해준다.


```java

public static final MyFragment newInstance(int title, String message) {
    MyFragment f = new MyFragment();
    Bundle bdl = new Bundle(2);
    bdl.putInt(EXTRA_TITLE, title);
    bdl.putString(EXTRA_MESSAGE, message);
    f.setArguments(bdl);
    return f;
}

@Override
public void onCreate(Bundle savedInstanceState) {
    title = getArguments().getInt(EXTRA_TITLE);
    message = getArguments().getString(EXTRA_MESSAGE);

    //...
    //etc
    //...
}

```