# Operation // Queue
- Operation은 GCD를 객체 지향적으로 재탄생시킨 것!
    - Operation을 사용하면 동시성 프로그래밍과 관련된 모든 작업들은 Operation이라는 객체로 만들어진다.
    - GCD처럼 OperationQueue라는 Queue에 넣어서 실행 및 관리 가능

```swift
import Foundation

let order1 = BlockOperation {
    print("돈까스")
    print("떡볶이")
}

let order2 = BlockOperation {
    print("튀김 우동")
}

let order3 = BlockOperation {
    print("알리오 올리오")
    print("생맥주 2")
}

let order4 = BlockOperation {
    print("과일 세트")
    print("LA 갈비")
}

let order5 = BlockOperation {
    print("김치전")
    print("바닐라 아이스크림")
}

let orderBar = OperationQueue()
orderBar.maxConcurrentOperationCount = 2

orderBar.addOperation(order1)
orderBar.addOperation(order2)
orderBar.addOperation(order3)
orderBar.addOperation(order4)
orderBar.addOperation(order5)
```
간단하게 만들었을경우
```swift
돈까스
튀김 우동
떡볶이
알리오 올리오
생맥주 2
김치전
과일 세트
바닐라 아이스크림
LA 갈비
순서는 위에서부터 2개씩 나타나게 된다.
```

##### Operation 만들기
- class BlockOperation: Operation
```swift
let operation = BlockOperation {
    //code
}
```

##### Operation의 프로퍼티
`Operation` 에는 해당 `Operation`상태를 추적할 수 있는 프로퍼티가 존재 합니다. GCD와의 차별화되는 강점!
```swift
var isCancelled: Bool  -> 취소네? 굳
var isExecuting: Bool
var isFinished: Bool
var isConcurrent: Bool
var isAsynchronous: Bool
var isReady: Bool
var name: String?
대충 네이밍으로 추정해서 사용하자...
```
##### Operation 실행
```swift
직접실행
operation.star()

Queue로 실행하는것
let operationQueue = OperationQueue()
operationQueue.addOperation(operation)
OperationQueue에는 operation을 넣어주면 바로 실행됩니다.
```

##### Cancel
- Operation의 실행을 취소 할수있는 기능
    - `operation.cancel()`
취소를 진행시키는거 일수 있지만 정확하게는 `isCancelled` 프로퍼티의 값을 `True`로 변경해주는것이다. 실직적으로 코드 동작을 중단하는것은 아니다. 그래서 cancel() 호출후에 `isCancelled` 프로퍼티 추적해서 관리해야한다.. 흠 좋긴한데.. 귀찮네..

##### Dependency
- 중속성 `Operation` 인스턴스들 사이에 종속적인 관계를 만들어서 실행의 순서를 관리하도록 해줍니다. addDependency(_:) 메서드로 종속적인 관계를 만들어주면 해당 Operation은 자신이 종속된 Operation의 작업이 끝날 때까지 실행할 수 없게 됩니다

```swift
let yagom = BlockOperation {
    print("🐻🐻🐻🐻🐻")
}

let noroo = BlockOperation {
    print("🦌🦌🦌🦌🦌")
}

let odong = BlockOperation {
    print("🌳🌳🌳🌳🌳")
}

odong.addDependency(yagom)
yagom.start()
odong.start()
출력
🐻🐻🐻🐻🐻
🌳🌳🌳🌳🌳
```
야곰이 끝이 나야지 오동이 준비할수있다.
오동은 야곰에게 종속이 되었기때문

- 교착상태가 될수도있다.
```swift
odong.addDependency(yagom)
yagom.addDependency(noroo)
noroo.addDependency(odong)

이렇게하면 서로가 서로 끝나면하는거기때문에 실행할수가없다.
님선이여...
```
