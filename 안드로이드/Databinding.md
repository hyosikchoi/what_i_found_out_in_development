# xml상에서 databinding 을 통해서 dp 값을 지정 하는 경우 알아둬야 할 점

* @dimen 을 통해서 dp 값을 지정할 수 있지만 이는 **padding** 만 가능하다. **margin** 은 불가능하다.



# Recyclerview adapter 내에서 viewmodel 사용시 databinding 되게끔 하는 법

```
private lateinit var orderShippingViewModel: OrderShippingViewModel

private lateinit var lifecycleOwner: LifecycleOwner

fun setOrderShippingViewModel(orderShippingViewModel: OrderShippingViewModel , lifecycleOwner: LifecycleOwner) {
    this.orderShippingViewModel = orderShippingViewModel
    this.lifecycleOwner = lifecycleOwner
}

```

* viewmodel 만 셋팅 시킬게 아닌 **lifecycleOwner** 까지 받아야한다.

* 그래야 해당 viewmodel 의 livedata 나 stateflow 값을 제대로 databinding 이 가능해진다.
