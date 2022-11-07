# ListAdapter 사용시 리스트 영역 주의해야 할점.

* item의 visibility로 영역을 숨기려고 하지만 중간중간의 영역은 item이 리스트에 존재하는한 남아 있다.

* 이를 방지하기 위해 **FrameLayout** 을 **wrapContent** 로 item layout을 감싸고 item layout도 wrapContent로 지정하고 visibility 를 조정한다.

* 하지만 이또한 item이 너무 많을 시 Ui를 그릴 때 버벅이는 이슈가 발생할 수 있다.

* item이 너무 많다면 visibility보단 remove 와 submitList를 활용해서 item 갯수를 조절하는 방식으로 보였다 안보였다 하는 방식이 나을수도 있다.