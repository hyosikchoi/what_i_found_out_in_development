# RecyclerView를 사용하면서 Grid(2단,3단 이상 진열)형태의 Layout을 제공해줍니다.

* 2단,3단 진열하면서 디바이스 화면 가로 비율에 맞게끔 설정하는 방법

1. ViewHolder를 ConstraintLayout 으로 설정하고,width를 **match_parent** 로 지정해줍니다.

```
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:app="http://schemas.android.com/apk/res-auto">

    <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/white"
        >

        <ImageView
            android:id="@+id/iv_photo"
            android:layout_width="0dp"
            android:layout_height="0dp"
            android:scaleType="fitXY"
            android:layout_margin="0.5dp"
            app:layout_constraintDimensionRatio="1"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"/>

    </androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```

2. RecyclerView 에서 layoutManager 를 Grid로 설정하고 span_count를 설정하면,해당 span_count에 맞게끔 디바이스 가로를 나눠서 각각의 ViewHolder가 match_parent 길이로 채우게 됩니다.

```
<androidx.recyclerview.widget.RecyclerView
            android:id="@+id/rv_photo_list"
            android:layout_width="@dimen/constraint_match"
            android:layout_height="@dimen/constraint_match"
            android:layout_marginEnd="-0.5dp"
            android:layout_marginStart="-0.5dp"
            app:layoutManager="androidx.recyclerview.widget.GridLayoutManager"
            app:spanCount="3"
            tools:listitem="@layout/item_play_mnstargram_photo"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/top_navigation"
            app:layout_constraintBottom_toBottomOf="parent"
            />
```

**두가지 팁!**


1. ViewHolder의 이미지 가로 세로 비율을 지정하고 싶을 때

width,height 둘중 하나는 **match_parent** 여야 하며 , ConstraintLayout 기준으로

```
app:layout_constraintDimensionRatio="1"
```
Ratio 설정으로 가로:세로 비율을 지정할 수 있습니다.


2. Grid 사이에 Border를 그리고 싶을 때

ViewHolder에 margin혹은 padding값으로 조절을 해줍니다.

```
android:layout_margin="0.5dp"
```

**하지만!** 여기서 가로 양 끝에는 border가 생기지 않고 사이에만 생기기 원한다면

RecyclerView태그에도 ViewHolder에 지정해준 margin혹은 padding start,end값을 **-** 값으로 지정해줍니다.

```
android:layout_marginEnd="-0.5dp"
android:layout_marginStart="-0.5dp"
```
