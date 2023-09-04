셀 재사용

```swift
  override func prepareForReuse() {
        label.text = nil
        imageView.image = nil
    }
```
이런식으로 셀이 재사용 될때에 값을 nil로 변경해야지 세탁?이 되며 새로운 셀을 재사용 하게 된다.
하지않을경우 셀이 재사용 되면서 이전에 가지고 있던 데이터를 가지면서 새로운 데이터를 덮기때문에 셀이 깨지거나 이상한 화면이 나타나는 것을 확인 할 수있다.



translatesAutoresizingMaskIntoConstraints

기본적으로 translatesAutoresizingMaskIntoConstraints 속성은 true로 설정되어 있습니다.

그러나 Auto Layout을 사용하려면 translatesAutoresizingMaskIntoConstraints를 false로 설정해야 합니다. 이렇게 하면 Auto Layout 시스템이 인터페이스 요소의 위치와 크기를 동적으로 결정하게 할수있다.
Auto Layout은 다양한 제약 조건(Constraints)을 정의하여 인터페이스 요소들 간의 관계를 지정하고, 이를 기반으로 화면 크기나 장치의 회전 등 다양한 상황에 맞춰 인터페이스를 유연하게 조정할 수 있습니다.

translatesAutoresizingMaskIntoConstraints를 false로 설정하지 않으면, Auto Layout의 제약 조건들이 적용되지 않고 기본적인 frame-based 레이아웃 시스템으로 동작하게 됩니다. 이 경우, 인터페이스 요소들의 위치와 크기가 화면 크기나 상황에 따라 자동으로 조정되지 않으며, 수동으로 제약 조건을 추가해야 하므로 번거로워집니다.

따라서, Auto Layout을 사용하려면 translatesAutoresizingMaskIntoConstraints를 false로 설정하여 인터페이스 요소들을 유연하게 배치할 수 있도록 해야 합니다.

autoresizingMask는 superview가 변함에 따라 subview의 크기를 어떻게 할것인가이기 때문에, 이와 동일한 기능을 하는 autolayout에서 같이 사용된다면 충돌이 날 수 있는것 > 충돌 방지를 위해 Auturesizing을 사용하지 않는것으로 명시적 선언

스토리보드로 진행할경우 자동으로 flase이기에 문제가 되지않는다.
허나 코드베이스로 하게 될경우에는 false로 걸어주어 인터페이스 요소들을 동적으로 결정하게 할수있다.


