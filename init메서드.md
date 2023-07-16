


```swift
 private var customerQueue: CustomerQueue
    
    init(numberOfCustomers: Int) {
        self.customerQueue = CustomerQueue()
        generateCustomerQueue(numberOfCustomers)
    }
```
이렇게 init에서 메서드를 초기화 하여 사용 가능하다 `numberOfCustomers` 를 주기 때문에 

```swift
private let bank = BankService(numberOfCustomers: 5)
bank.start()
```
이렇게 메인에서 고객수를 정할수있으며 그 정한 수만큼 객체가 동작한다. 

```swift
class CustomerQueue {
    private var customers: Queue<Customer>
    
    init() {
        self.customers = Queue<Customer>()
    }
    
```

이렇게 `CustomerQueue` 를 init에서 초기화를 했기 때문에 가능한거다!!
