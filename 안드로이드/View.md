# View clipChildren 속성에 대해서 알아보자.

* 기본적으로 안드로이드의 모든 view는 자신이 물리적으로 차지하는 영역 만큼만 그릴 수 있다.

* 모든 view가 부모 view의 canvas를 넘겨받고, 그 canvas를 자신의 영역 만큼만 clip해서 사용한다. **이 clipping하는 과정으로 인해 자신이 차지하는 영역 밖으로는 아무것도 그리지 못한다.**

* 하지만 자신의 영역 밖에 그려야 할 상황도 있다. 이를 가능하게 해주는 속성이 **clipChildren** 이다.

* android:clipChildren="false" 해주면 부모 view 에서 **너의 사이즈만큼 clip하지 말고 그냥 내 canvas 그대로 써!** 라고 하게 되고 자신의 영역을 넘어가는 곳도 그릴 수 있게 해준다. [참조](https://giantsol.github.io/android-clipchildren/)
 
