# Card 컴포넌트에서 radius 및 백그라운드 컬러 변경 하는 법

```kotlin

 Card(
    modifier = Modifier.align(Alignment.TopStart),
    shape = RoundedCornerShape(6.dp),
    colors = CardDefaults.cardColors(
        containerColor = MaterialTheme.aceColorScheme.newOp
        )
    )

```

* shape 에 RoundedCornerShape 속성 을 주면 radius 를 지정할 수 있다.

* colors 속성에 CardDefaults.cardColors 의 containerColor 를 통해 백그라운드 색상을 변경할 수 있다.