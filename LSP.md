### 리스코프치환의 법칙(LSP)

- 상속에 있어서 가장 중요한 기본 원칙 제시
- OCP를 가능하게 해주는 원칙
- 잘못된 상속

- 잘못된 상속은 LSP를 위반 하는 경우가 많음
- 상속을 하다보면 LSP를 위반하게된다…
- 위반 할 수 밖에 없게 만듦…
- 상속할 때 해서는 안되는 행위

- 부모의 행위를 자식이 거부한다?.
- 퇴화 함수(오버라이드 한다음에 그 기능을 못쓰게하는거? 에러를 던지거나? 기능 구현지우기?)
- ex) 직사각형과 정사각형은 어떤 상속 구조를 가지나?

직사각형을 상속 받은 정사각형
정사각형을 상속 받은 직사각형
-> 둘 사이에는 상속 관계가 있으면 안된다.

직사각형과 정사각형
일반적인 관념과 상충
직사각형과 정사각형의 관계 
일반적인 관념 상 정사각형은 직사각형의 한 종류
부모(직사각형)를 상속받은 자식(정사각형)은 당연해 보임
만일 setWidth 함수가 있다면
정사각형의 경우 height도 같이 바꿔야 한다.
직사각형은 setWidth로 폭을 2배로 하면 면적이 2배가 됨
정사각형은 setWidth로 폭을 2배로 하면 면적이 4배가 됨
부모의 정합성을 깨버린다
이 경우 자식이 거부 할 수박에 없는 기능을 부모가 제공하고있다.
와 이부분 어렵다…

### 상속에 관해 생각해보기
- 개,고양이에게 “걷기”, “뛰기” 행위를 추가하면 그 행위를 동물 레벨로 올릴 수 없음
- 붕어나 고래는 “걷기”. “뛰기” 를 주면 퇴하 한다… (쓸수없기에…)
- 동물의 상속 구조에서 “걷기”, "뛰기"의 행위는 상속 구조 자체에 넣을 수 없다.
- “걷기”, “뛰기”, "헤엄치기"등의 행위는 상속과 별도로 존재해야한다.

### 어떤 문제가 있나?
- LSP가 위반되고 있어도 UIKit을 사용하는데 큰불편함은 없다
- View 중에 size를 바꿀 수 없는 것이 있다는 것을 경험과 학습을 통해서 배운다?..
- 하지만 이런 경우가 매우 많다면 코딩하기 힘들어짐
- ???: 클래스의 장점이 뭐야? -> 상속 단점이 뭐야? -> 상속… 어렵다…

### LSP를 위반하게 되면
- 모든 클래스에서 하위 클래스를 명시적으로 지정해서 코딩해야한다.
-OCP를 사용할 수 없게됨
- 코드의 복잡도를 높임
- 부모 클래스가 자식 클래스를 알아야 하는 경우도 발생
- 대부분의 경우 LSP를 위반하지 않기 때문에
- 복잡한 상속 관계를 가지는 프레임웍을 사용하면서도 부모 클래스의 동작을 당연히 해줄 것으로 믿고 작업할 수 있음
- 대부분의 경우 LSP를 잘 지켜주고 있다.
- 잘 지키게 되면 -> 상위 클래스를 기준으로 작성된 코드가 문제 없이 동작 된다
- 추상화 된 인터페이스 하나로 공통의 코드를 작성 할 수 있음
- 상속된 수많은 다른 클래스를 일일이 고민하지 않는다

### 간단하게 솔리드에서 리스코프 치환을 작성해봐라 하면?
- 부모의 기능을 오버라이딩 하여 퇴화 시킨다
- 부모의 기능을 받아 쓰지 못한다면 의미가 없다 (새로 정의 및 재정의??)
- 부모 클래스가 자식클래스을 알아야지 작동하게 한다? 흠?? 역공격…
- 코드가 많이 좋지 않기때문에 오픈 개방이 제대로 안되어 캡슐화 은닉화 부분이 잘 안되게된다?


### 현실적인 이야기?
- 모든 코드에서 LSP를 지키기는 어려움
- 적정선에서 trade-off
- 하지만 그 부분은 나중에 문제를 일으킬 수 있음
- LSP를 이해하고 따르면
- 설계에 도움이 됨
- 발생할 문제를 사전에 막을 수 있음
-복잡하고 이해할 수 없는 상속을 만들지 않게 함
