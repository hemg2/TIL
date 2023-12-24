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
