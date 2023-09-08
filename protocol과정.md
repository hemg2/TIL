- 프로토콜 생성후 구현 진행
```swift
protocol DateFormattable {
    func formattedDate(from date: Date) -> String
}

extension DateFormattable {
    func formattedDate(from date: Date) -> String {
        let formatter = DateFormatter()
        formatter.dateStyle = .long
        formatter.timeStyle = .short
        formatter.locale = Locale(identifier: "ko_kr")
        formatter.dateFormat = "yyyy/MM/dd"
        return formatter.string(from: date)
    }
}
```

 - 뷰컨 또는 셀에서 사용 예시
 
```swift
class TableViewCell: UITableViewCell, DateFormattable {
    func setModel(_ sample: Sample) {
        dateLabel.text = formattedDate(from: sample.createdAt)
    }
}
// ViewController.swift
class ViewController: UIViewController, DateFormattable {
    func updateDateLabel(with date: Date) {
        dateLabel.text = formattedDate(from: date)
    }
}
```


## 채택하지 않고 구현부의 인스턴스를 생성하여 사용하는경우 
- 이런 방식으로 코드의 결합도를 낮추고, 필요한 객체에 필요한 구현을 주입함으로써 유연성을 높일 수 있습니다. 하지만 의존성이 높다
```swift
class DateFormatterManager: DateFormattable {
    private let formatter: DateFormatter = {
        let formatter = DateFormatter()
        formatter.dateStyle = .long
        formatter.timeStyle = .short
        formatter.locale = Locale(identifier: "ko_kr")
        formatter.dateFormat = "yyyy/MM/dd"
        return formatter
    }()
    
    func formattedDate(from date: Date) -> String {
        return formatter.string(from: date)
    }
}
```

```swift
class TableViewCell: UITableViewCell {
    var dateFormattable: DateFormattable = DateFormatterManager()
    
    func setModel(_ sample: Sample) {
        dateLabel.text = dateFormattable.formattedDate(from: sample.createdAt)
    }
}

class ViewController: UIViewController {
    var dateFormattable: DateFormattable = DateFormatterManager()
    
    func updateDateLabel(with date: Date) {
        dateLabel.text = dateFormattable.formattedDate(from: date)
    }
}
```

## 위의 예시와 같이 (의존성을 주입 하지 않은 경우)
```swift
class MainViewController: UIViewController {
    private let usecase = MainViewControllerUseCaseImplementation()
    // ... 채택하지않고 프로토콜 구현부을 인스턴스로 생성하게되는 경우
}
```
이 방식에서는 MainViewController 클래스가 직접 MainViewControllerUseCaseImplementation 클래스의 인스턴스를 생성하고 사용합니다. 이것은 `강한 의존성`을 나타냅니다. 클래스가 자신의 의존성을 직접 관리하므로 클래스의 코드가 MainViewControllerUseCaseImplementation에 `강하게 결합`되어 있습니다. 이로 인해 다음과 같은 문제가 발생할 수 있습니다

테스트하기 어려움: MainViewController를 테스트할 때, MainViewControllerUseCaseImplementation에 대한 목 객체(Mock)를 주입하기가 어려울 수 있습니다.
유연성 부족: 나중에 MainViewControllerUseCase의 다른 구현체를 사용하거나 변경하려면 MainViewController 클래스의 코드를 직접 수정해야 합니다.


# 의존성 주입하게되는경우
- 프로토콜을 중심으로 의존성을 관리하고 코드의 모듈화 및 재사용성을 높일 수 있습니다.

```swift
class MainViewController: UIViewController {
    private let usecase: MainViewControllerUseCase
    
    init(usecase: MainViewControllerUseCase) {
        self.usecase = usecase
        super.init(nibName: nil, bundle: nil)
    }
}
```

이 방식에서는 MainViewController 클래스가 외부로부터 MainViewControllerUseCase 인스턴스를 주입받습니다. 이것은 `약한 의존성`을 나타냅니다. 클래스는 의존성을 직접 생성하지 않고 외부로부터 주입받아 사용합니다. 

테스트 용이성: 테스트할 때 목 객체(Mock)를 주입하여 테스트하기 쉽습니다.
유연성: 나중에 다른 MainViewControllerUseCase 구현체를 사용하거나 변경할 때 클래스 코드를 수정하지 않고 새로운 구현을 주입할 수 있습니다.
의존성 주입을 사용하면 코드의 결합도를 낮추고 테스트와 유지보수를 쉽게 할 수 있으며, 클래스의 재사용성과 확장성을 향상시킬 수 있습니다.

---
프로토콜 의존성 주입 패턴을 하여 진행하게 된다면 장점.
유연성 및 확장성: 프로토콜을 사용하면 클래스가 특정 구현체에 `의존`하지 않고 프로토콜에만 `의존`하므로 새로운 구현을 쉽게 교체하거나 추가할 수 있습니다.
테스트 용이성: 의존성 주입을 통해 테스트할 때 모의 객체(Mock)를 주입하여 테스트하기 용이합니다.
의존성 역전 원칙(Dependency Inversion Principle) 준수: 고수준 모듈이 저수준 모듈에 의존하지 않고, 둘 모두 추상화(프로토콜)에 의존해야 한다는 객체지향 설계 원칙을 따릅니다.
코드 재사용성: 동일한 프로토콜을 여러 클래스에서 사용할 수 있으므로 코드 재사용성이 높아집니다.
유지보수 용이성: 구현부를 분리하여 관리하면 유지보수가 쉬워집니다. 특히 여러 클래스에서 동일한 인터페이스를 사용할 때 유용합니다.
