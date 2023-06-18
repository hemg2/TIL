DIP 의존역전의 법칙




의존 관계는 단방향으로 설계 되어야한다

classA -> classB -> classC  이거다.

classA -> classB -> classC -> classA  이건 잘못 되었다.(어느 클래스도 독립적으로 사용되지 못한다.)

그렇치만 만약에 classC 가 classA 혹은 classB 에 의존해야하는 상황이라면 DIP가 해결책이다??



의존 관계는 어떤 방향으로 흘러가야 하는가?
- 구체적인 부분에서 추상적인 방향으로 의존관계를 가져야 함
- 추상적인 것이 구체적인 것에 의존하지 않아야 함

정책이 구체적인 것에 의존하는 경향
- 정책은 추상적인 것이다.

상위 수준은 하위 수준에 의존하면 안됨
- 상위 수준: 추상적인 부분
- 하위 수준: 구체적인 부분 

iOS에서의 대표적인 예 DIP
(UITableView 의 코드는 개발자가 커스텀한 커스템셀에 직접적으로 의존하지 않는다. 대신 cell의 추상적인 레벨인 UITableViewCell을 사용한다 )
- UITableView: 추상적임
- UITableView 를 이용해서 구현된 코드 및 Cell : 구체적임
- UITableView 는 직접적으로 사용자의 CustomCell을 참조하지 않음(의존없음)
- 사용자가 작성한 코드(구체적인)는 UITableView와 UITableViewCell(추상적인)에 의
- 추상적인 부분이 구체적인 부분에 동작을 위임(delegate, dataSource) (동작에있어서 구체적인 부분이다)
- 직접적으로 의존하지 않고 인터페이스에 의해 의존함


또 다른 예시)
- UIViewController 와 MyViewController
- UIViewController는 View-life-cycle에 대한 정책결정
- MyViewController는 구체적인 구현
- MyViewController는 UIViewController에 의존하지만 UIViewController는 MyViewController에 의존하지 않음
- 



DIP
- 소프트웨어 모듈들을 분리하는 원칙, 상위계층(정책결정)이 하위계층(세부사항)에 의존하는 전통적인 의존관계를 반전(역전)시켜 상위계층이 하위 계층의 구현으로 부터 독립하게 함
- 상위모듈은 하위모듈에 의존해서는 안된다. 상위모듈과 하위모듈 모두 추상화에 의존해야 한다.
- 추상화는 세부사항에 의존해서는 안된다. 세부사항이 추상화에 의존해야 한다.

꼭 protocol을 사용하는 것 만이 DIP는 아니다
상속에서 super class는 추상적인 개념 sub class는 구체적인 개념
Super class의 추상적인 로직은 sub class에 의존하지 않고 작성되어야 함
세부 사항에 의존하지 않음
LSP와 개념적으로 유사한 부분이 있음
구체화를 위해서 sub class는 super class의 메소드를 override 한다.

- Hollywood원칙
- 영화에 출연하고 싶으면 연락처를 주고 가세요 (먼저 연락하지 마세요.), 필요하면 저희가 연락드리겠습니다.
- UITableView 사용에서도 동일한 형태를 보인다.

의존 관계를 역전시켜서 얻을 수 있는 것
- 두 모듈간의 의존관계를 단방향으로 만들어줌
- 추상화된 부분의 코드는 재활용성 증가
