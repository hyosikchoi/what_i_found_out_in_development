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


# 각 ViewHolder 에서 item 이미지 크기 비율에 맞게끔 Height 자동 조절 되게 하는 방법. 

* 1. ImageView 의 layout_height 를 **wrap_content** 로 지정하여 이미지의 크기에 따라 
동적으로 처리하게끔 한다.

* 2. 1의 방법으로 통해 Height 가 동적으로 변하기는 하지만 width 를 가득 채우면서 그에 맞는 비율로 동적으로 height 가 늘어나진 않는다. width 를 가득 채우면서 동적으로 늘어나게 하려면 **adjustViewBounds** 속성을 **true** 로 주면 된다.

```
 <androidx.appcompat.widget.AppCompatImageView
        android:id="@+id/iv_photo"
        android:layout_width="@dimen/constraint_match"
        android:layout_height="wrap_content"
        android:adjustViewBounds="true"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:src="@drawable/img_placeholder_goods_375" />
```


# RecyclerView 하단의 Padding 을 주고 해당 Padding 영역도 Scroll 되게끔 하는 법.

* RecyclerView 태그에 Padding 값을 준 이후에 **android:clipToPadding="false"** 속성을 주면 된다. 


# RecyclerView 데이터 갱신마다 스크롤 위치 저장했다가 갱신하는 방법 (데이터 갱신마다 스크롤 위치가 변경 되는 이슈 때문) [참조](https://stackoverflow.com/questions/28658579/refreshing-data-in-recyclerview-and-keeping-its-scroll-position) 

```
// 데이터 갱신 전에 Save state 
private Parcelable recyclerViewState;
recyclerViewState = recyclerView.getLayoutManager().onSaveInstanceState();

// 데이터 갱신 후 Restore state
recyclerView.getLayoutManager().onRestoreInstanceState(recyclerViewState);
```