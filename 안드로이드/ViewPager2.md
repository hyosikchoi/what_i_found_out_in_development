# ViewPager2 사용시 ViewHolder 영역 주의해야 할점.

```kotlin
LayoutInflater.from(context).inflate(resource, this, attachToRoot)
```

* attachToRoot 값은 **false** 여야 하며 , ViewHolder의 width , height 값은 **match_parent** 여야 합니다.

* 그렇게 하지 않을 시 java.lang.IllegalStateException: Pages must fill the whole ViewPager2 (use match_parent) 이와 같은 에러가 발생합니다.