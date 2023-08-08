

```swift
struct 주문 {
    let orderID: Int  // 주문번호
    let product: String //품명
    let quantity: Int //수량
}


class 주문내역 {
    func logOrder(_ order: 주문) {
        print("Order logged: \(order)")
    }  // 주문 기록만한다 주문 객체를 받아서 내역 출력하기
}


class 주문처리 {
    let orderLogger: 주문내역
    
    init(orderLogger: 주문내역) {
        self.orderLogger = orderLogger
    }
    
    func processOrder(order: 주문) {
        orderLogger.logOrder(order)
    }
}
```


```swift
let orderLogger = 주문내역()
let orderProcessor = 주문처리(orderLogger: orderLogger)


let order = 주문(orderID: 1, product: "mac", quantity: 1)
let order1 = 주문(orderID: 2, product: "iPhone", quantity: 2)
orderProcessor.processOrder(order: order)
orderProcessor.processOrder(order: order1)
```

```swift
Order logged: 주문(orderID: 1, product: "mac", quantity: 1)
Order logged: 주문(orderID: 2, product: "iPhone", quantity: 2)
```




..... 어 어렵다...



```swift 어떤 서버와의 통신을하고있느곳 URLSession의 저장소 그냥 URPSession로직을 가지고있다.
protocol URLSessionProvider {}
class URLSessionProviderImplementation: URLSessionProvider {}
```

- 저장소  -> 액션하기 서버와 통신을 진행한다. 요청 데이터를 하여 진행 디코딩도 진행하는중  URLSessionProvider의존하고있다
```swift  
protocol Repository {}
final class RepositoryImpl: Repository {}
```

- 저장소에 있는것을 가져와서 액션을진행 뷰컨이 useCase를 알고있기에 여기가 뷰의모델역활을한다.
  Respository의 의존성을 주입받음
```swift  
protocol UseCase {}
final class UseCaseImpl {
let Repository: Repository
}
```

- 뷰컨에 업데이트 진행
```swift 
protocol MainViewControllerUseCaseDelegate: AnyObject {}
class MainViewController: MainViewControllerUseCaseDelegate {
}
```



```swift
 let sessionProvider: URLSessionProvider = URLSessionProviderImplementation()
        let boxOfficeRepository: BoxOfficeRepository = BoxOfficeRepositoryImplementation(sessionProvider: sessionProvider)
        var usecase: MainViewControllerUseCase = MainViewControllerUseCaseImplementation(boxOfficeRepository: boxOfficeRepository)
        let mainViewController = MainViewController(usecase)
```

계속 보다보니깐 조금씩 이해가 +1씩 되면서 점점알아가고 있는거같다.
