# withLatestFrom 에 대해 알아보기. [참조 링크](https://fomaios.tistory.com/entry/RxSwift-Combining-Observables-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-Combine-LatestZip-MergeConcatwithLatestFrom)


* 만약 버튼과 텍스트필드가 있고 버튼을 눌렀을때 텍스트필드의 값을 방출한다고 가정할때
* 우리는 텍스트필드의 맨 마지막 데이터를 원할 것입니다.
* 그럴때 알맞는 연산자라고 볼 수 있습니다.


**즉, 버튼과 텍스트필드값 두개의 Observable에서 텍스트 필드값을 아무리 onNext해도 버튼을 onNext했을 때의 최신 텍스트 필드값에 onNext한 값이 방출 되게 됩니다.** 

* 예제 코드

```kotlin
let button = PublishSubject<Bool>()
let textField = PublishSubject<String>()

let withLatestFrom = button.withLatestFrom(textField)
withLatestFrom.subscribe({print($0)})

textField.onNext("S")
textField.onNext("Swi")
button.onNext(true)
textField.onNext("Swif")
textField.onNext("Swift")
button.onNext(true)
//next(Swi)
//next(Swift)

```