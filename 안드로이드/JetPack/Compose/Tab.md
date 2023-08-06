# TabRow 를 감싸는 Layout 으로 Scaffold 는 해서는 안된다.

```kotlin
Scaffold(
    modifier = Modifier.fillMaxSize(),
) {
    val pagerState = rememberPagerState()
    val coroutineScope = rememberCoroutineScope()
 
    TabRow(
        selectedTabIndex = pagerState.currentPage,
        indicator = { tabPositions ->
            TabRowDefaults.Indicator(
                Modifier.pagerTabIndicatorOffset(pagerState, tabPositions)
            )
        }
    ) {
        pages.forEachIndexed { index, title ->
            Tab(
                text = { Text(text = title) },
                selected = pagerState.currentPage == index,
                onClick = {
                    coroutineScope.launch {
                        pagerState.scrollToPage(index)
                    }
                },
            )
        }
      }

    HorizontalPager(
        count = pages.size,
        state = pagerState
    ) {
        when(pagerState.currentPage) {
            0 -> {
                MemoScreen(viewModel = viewModel)
            }
            1 -> {
                ImportantMemoListScreen()
            }
        }
    }
}
```

* 위의 코드와 같이 Scaffold 로 감싸게 된다면 Tab 이 제대로 인식 되지 않는다.

* **Column** 을 사용해줘야 한다. 