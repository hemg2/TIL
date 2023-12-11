- github
https://github.com/pointfreeco/swift-composable-architecture#Installation <br>

- The Composable Architecture는 각 기능을 아주 작은 단위로 분리하여 구현하고 적재적소에 레고처럼 조립할 수 있는 모듈형 아키텍처 패턴입니다.
- TCA는 값 타입에 기반하여 각 객체를 모듈화하고 애플리케이션 전체의 상태를 일관적으로 관리할 수 있게 표준을 제한한다. 최소 기능 단위로 구성된 각 Unit 객체는 다른 기능으로의 결합-분리를 쉽게 할 수 있습니다.

- TCA에 요구되는 사전 습득 지식 4가지
    - Swift 타입의 대한 이해
        - 1. 필요: 값 타입과 참조 타입을 비교할 수 있는 수준
        - 2. 충분: 타입 파라미터에 대해 간단히 설명 할 수 있는 수준
    - SwiftUI에 대한 기본적인 이해
        - 1. 필요: View를 렌더링하기 위해 @State, @Published등의 프로퍼티 래퍼 혹은 @Observable 매크로를 써야하는 이유에 대해서
    - inout 키워드에 대한 이해
        -  1. 필요: 파라미터로 전달된 값을 타입을 변형할 수 있는 수준
        -  2. 충분: copy-in copy-out 구조에 대해 설명할 수 있는 수준
    - KeyPath 에 대한 이해
        - 1. 필요: KeyPath에 대해 들어보고 예시 코드를 읽을 수 있는 수준
        - 2. 충분:KeyPath를 활용하여 타입에 대한 key-value 접근을 구현할 수 있는 수준

