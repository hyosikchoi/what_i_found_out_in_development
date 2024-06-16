# BottomSheet 에서 특정 컨텐츠 클릭해서 hide() 시키는 방법

```kotlin

var isShowDistribution by remember {
    mutableStateOf(false)
}

val sheetState = rememberModalBottomSheetState(
        skipPartiallyExpanded = true,
    )

 Image(
    modifier = Modifier.clickable(
    onClick = {
        coroutineScope.launch {
            sheetState.hide()
        }.invokeOnCompletion {
            isShowDistribution = false
          }
        },
    indication = null, // 클릭 이펙트 제거
    interactionSource = remember {
            MutableInteractionSource()
        }
    ),
    painter = painterResource(id = if (CommonUtil.isBlackMode()) R.drawable.ic_close_24_night else R.drawable.ic_close_24),
    contentDescription = "닫기"
)

```

* Modifier.clickable 속성을 통해 onClick 에서 위의 코드와 같이 실행한다. invokeOnCompletion 을 통해 hide 후 BottomSheet의 show를 결정 하는 변수를 false 로 만들어 준다.

* indication = null 과 interactionSource 속성을 통해 클릭 이펙트를 제거할 수 있다.