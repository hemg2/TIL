## lazy 지연저장 프로퍼티?
lazy 키워드를 사용하는 프로퍼티를 지연 저장 프로퍼티(Lazy Stroed Property)라고 합니다.
지연 저장 프로퍼티는 호출이 있어야만 값을 초기화 하는 특성을 가지고 있습니다.

다중 스레드 환경에서 지연 저장 프로퍼티에 동시다발적으로 접근할 때는 한 번만 초기화된다는 보장이 없습니다.
생성되지 않은 지연 저장 프로퍼티에 많은 스레드가 비슷한 시점에 접근한다면, 여러 번 초기화될 수 있습니다.

우리가 인스턴스를 초기화 하는 과정에서 
언제나 모든 저장 프로퍼티가 동시에 초기화 될 필요가 없는 상황이 분명히 있겠지요?
그럴 때 지연 저장 프로퍼티 즉, lazy를 사용해 주시면 호출이 있을 때만 값을 초기화 하기 때문에
불필요한 성능저하나 공간 낭비를 줄일 수 있습니다!


```swift
 var fruitAndLabel: [Fruit: UILabel] = [
        .strawberry: strawberryStockLabel,
        .banana: bananaStockLabel,
        .pineapple: pineappleStockLabel,
        .kiwi: kiwiStockLabel,
        .mango: mangoStockLabel
    ]
```
위와 같은 코드를 진행할경우 에러가 나타난다.
아울렛을 잡아 놨지만 같은 함수안에서 가 아닌 클래스안에서 지역으로 설정할 경우 쓸수없다고한다.
에러는 우선은 레이블 값을 사용할수 없다고 나타날 것이며, 이니셜라이저가 'self'를 사용할 수 있기 전에 실행됩니다.
아직 셀프로라도 사용할수 없기 때문인거 같다.

```swift
 lazy var fruitAndLabel: [Fruit: UILabel] = [
        .strawberry: strawberryStockLabel,
        .banana: bananaStockLabel,
        .pineapple: pineappleStockLabel,
        .kiwi: kiwiStockLabel,
        .mango: mangoStockLabel
    ]
```
이렇게 lazy를 사용해서 인스턴스 값이 호출될때 값을 초기화 할때 사용이 됩니다.
그러니깐 미리 변수를 지정해 놓고 이후 값이 초기화, 변화 할때 그때 사용 된다는 점입니다.
