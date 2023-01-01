# ListAdapter 사용시 리스트 영역 주의해야 할점.

* item의 visibility로 영역을 숨기려고 하지만 중간중간의 영역은 item이 리스트에 존재하는한 남아 있다.

* 이를 방지하기 위해 **FrameLayout** 을 **wrapContent** 로 item layout을 감싸고 item layout도 wrapContent로 지정하고 visibility 를 조정한다.

* 하지만 이또한 item이 너무 많을 시 Ui를 그릴 때 버벅이는 이슈가 발생할 수 있다.

* item이 너무 많다면 visibility보단 remove 와 submitList를 활용해서 item 갯수를 조절하는 방식으로 보였다 안보였다 하는 방식이 나을수도 있다.



# Multi ViewHolder 사용시 SealedClass 활용법

* 하나의 API를 통해 두가지 타입의 데이터로 가공하여 사용해야 할 경우 SealedClass로 부모 타입의 리스트로 만들어 해당 리스트 안에 두가지 타입의 데이터를 가지고 있게 할 수 있다.

```kotlin
sealed class DiseaseListModel {

    data class DiseaseCategoryModel(
        val categoryName : String,
        val categoryCode : String,
        val type : String,
        // 확장 여부
        val isExpandable : Boolean = false
    ) : DiseaseListModel()

    data class DiseaseModel(
        val categoryName : String,
        val categoryCode : String,
        val type : String,
        val id : Int,
        // etc 내용
        val etcText : MutableLiveData<String> = MutableLiveData(null)
        // 체크 상태 여부
        val isChecked : Boolean = false
    ) : DiseaseListModel()

}
```

* 위의 예시는 질환 리스트를 아코디언 메뉴로 만들 때 **질환 헤더 타입**과 **질환 내용 타입** 두 종류를 질환 리스트를 상속받게 만들었다.