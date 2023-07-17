# LazyColumn 에서 StickyHeader 생성 하는법


* Compose 에서는 아직은 experimental(실험적) 이지만 자체적으로 stickyHeader 를 제공하고 있습니다.

```kotlin

@OptIn(ExperimentalFoundationApi::class)
@Composable
fun MessageList(messages: List<Message>, onDeleteClicked: (Message) -> Unit) {
    LazyColumn {
        messages.forEach { message ->
            stickyHeader {
                StickyHeader(message.id)
            }
            item(
                key = message.id
            ) {
                MessageRow(msg = message, onDeleteClicked = onDeleteClicked)
            }
        }
    }
}

```

* 이런식으로 LazyColumn 내부에서 List의 반복문을 통해 **stickyHeader** 를 지정해줄 수 있습니다.