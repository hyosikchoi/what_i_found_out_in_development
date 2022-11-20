# xml상에서 databinding 을 통해서 dp 값을 지정 하는 경우 알아둬야 할 점

* @dimen 을 통해서 dp 값을 지정할 수 있지만 이는 **padding** 만 가능하다. **margin** 은 불가능하다.



# Recyclerview adapter 내에서 viewmodel 사용시 databinding 되게끔 하는 법

```kotlin
private lateinit var orderShippingViewModel: OrderShippingViewModel

private lateinit var lifecycleOwner: LifecycleOwner

fun setOrderShippingViewModel(orderShippingViewModel: OrderShippingViewModel , lifecycleOwner: LifecycleOwner) {
    this.orderShippingViewModel = orderShippingViewModel
    this.lifecycleOwner = lifecycleOwner
}

```

* viewmodel 만 셋팅 시킬게 아닌 **lifecycleOwner** 까지 받아야한다.

* 그래야 해당 viewmodel 의 livedata 나 stateflow 값을 제대로 databinding 이 가능해진다.


# BaseObservable() 을 통해 databinding을 Observable 형태로 사용할 수 있다.

1. **Observable** 형태로 사용할 데이터를 지정한다.


```kotlin
class DiseaseListObservable : BaseObservable() {

    private var diseaseList : List<DiseaseListModel> = emptyList()

    @Bindable
    fun getDiseaseList() : List<DiseaseListModel> = this.diseaseList

    fun setDiseaseList(diseaseList : List<DiseaseListModel>) {
        this.diseaseList = diseaseList
        notifyPropertyChanged(BR.diseaseList)
    }

}
```

2. layout 에 observe 할 데이터를 지정한다.

```
<?xml version="1.0" encoding="utf-8"?>
<layout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    >

    <data>

        <variable
            name="diseaseList"
            type="kr.co.fitpet.features.pet.play.model.DiseaseListObservable"/>

        <variable
            name="diseaseCategory"
            type="kr.co.fitpet.features.pet.play.model.DiseaseListModel.DiseaseCategoryModel" />

    </data>

    <androidx.constraintlayout.widget.ConstraintLayout
        android:id="@+id/cl_disease_header_root"
        android:layout_width="match_parent"
        android:layout_height="54dp"
        android:background="@drawable/ripple_white"
        android:clickable="true"
        android:focusable="true"
        android:padding="16dp">

        <androidx.appcompat.widget.AppCompatTextView
            android:id="@+id/tv_header_title"
            style="@style/pretendard_bold_16"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@{diseaseCategory.categoryName}"
            android:textColor="@color/fitpet_gray_900"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            tools:text="피부" />

        <androidx.appcompat.widget.AppCompatTextView
            android:id="@+id/tv_disease_count"
            style="@style/pretendard_regular_12"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            app:set_count="@{diseaseList.diseaseList}"
            app:category="@{diseaseCategory.categoryName}"
            android:background="@drawable/ic_disease_count_background"
            android:visibility="gone"
            android:gravity="center"
            android:textColor="@color/white"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintStart_toEndOf="@+id/tv_header_title"
            app:layout_constraintTop_toTopOf="parent"
            tools:text="1" />

        <androidx.appcompat.widget.AppCompatImageView
            android:id="@+id/iv_arrow"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:rotate="@{diseaseCategory.expandable}"
            android:src="@drawable/ic_disease_arrow_down"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintTop_toTopOf="parent" />


    </androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```




