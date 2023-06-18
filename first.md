FIRST 원칙

- Fast: 빠르게
- 빠르게 동작해야한다 테스트 코드는 세분화되어있다  단순하게 짜더라도 세분화 시켜놓는다  안정성과 생산성이 있다 근데 생산성에 어긋난다.


- Independent / lsolated: 독립적으로  
- 테스트 를진행시 a와 b가 서로 영향을 미쳐서는 안된다.
- 신발 젖는 테스트 미끄럼 테스트 -> 물을 부어 놓으면??? 그럼 젖고 미끄러지니깐 독립적인게 아니다. 서로 하나씩 테스트 한다

- Repeatable: 반복 가능하게
- 반복을 어떤식으로해도 같은 결과 값이 나와야한다.
- 네트워크 환경? 인터넷 연결 상태의 테스트 연결 안된 상태의 테스트는 결과가 다르다 그럼 이게 반복가능한테스트가 아니다
- 다른 환경 요소들에 영향을 받으면 안된다.

- self-validating: 스스로 검증하는
-  a에서 테스트 하고싶은게 a에 다있어야한다. 내부에 모든것이 있어야한다 당연한거다.


- Timely: 적시에 
- 언제 쓸래? 구현하면서 테스트 한다? 코드 작성직전, 작성하면서, 구현 완료후에 테스트
- 구현하기전에 테스트를 하는것이 좋다
- 테스트가 개발을 주도 한다 구현하기전에 테스트를 한다 tdd 


```swift
import XCTest
@testable import UnitTestSample(프로젝트명)

final class 클래스명+Tests: XCTestCase {
var sut: 객체명! (테스트를 하기위해 ! 사용..)

   override func setUpWithError() throws {
        try super.setUpWithError()  시작하는부분
        sut = LottoMachine()
    }
    
    override func tearDownWithError() throws {
        try super.tearDownWithError()
        sut = nil   닐 선언을 해주아야한다.
    }

func test_메소드명() {  test_ 라는 네이밍으로 시작한다.
given, when, then 으로 나누어야한다.
 	 // given   
        let input = [3, 6, 9]
        
        // when              int값이 6개 이상인가? -> false 3개니깐   
        let result = sut.isValidLottoNumbers(of: input)
        
        // then
        XCTAssertFalse(result)  result가 false를 반환하는가?
반대인 XCTAssertTrue(result) 도 있다.
}

 func test_countMatchingNumber_테스트2개같음() throws {
        let input = [1, 2, 3, 4, 5, 6]
        let input2 = [1, 2, 43, 44, 45, 40]
        
        let result = try sut.countMatchingNumber(user: input, winner: input2)
             input 값 2개를 같게 했으며 XCTAssertEqual 진행시 result값과 2개의 값이 같다는걸 테스트한다.
        XCTAssertEqual(result, 2) -> 값 2개가 같은지 확인한다.
    }

} 
```




```swift
func test_countMatchingNumber_테스트3개같나() {
        //given
        let input = [1, 2, 3, 4, 5, 6]
        let input2 = [1, 2, 3, 44, 45, 40]
        
        // when
        var result: Int = 0
        do {
            result = try sut.countMatchingNumber(user: input, winner: input2)
            // then
            XCTAssertEqual(result, 3) //여기가 3개면 밑에 실행안됨
        } catch {  위에 3개가 아니라면 catch 문이 실행되면서 문제점을 찾게 된다.
            XCTAssertFalse(true)
            XCTAssertEqual(error as? LottoMachineError, LottoMachineError.invalidNumbers)
        }
    }
```


## 야곰닷넷
FIRST 원칙
좋은 유닛 테스트를 위해 지켜야 하는 것으로 소개되는 FIRST라는 원칙이 있습니다. 테스트 코드를 작성하실 때 천천히 생각해 보시면 좋을 것 같아요 🙂
* Fast 테스트는 빠르게 동작할 수 있어야 합니다. 실제 프로젝트에서는 수많은 테스트 코드를 작성하게 될 텐데 테스트가 느리게 동작한다면 테스트를 실행하는 데에만 몇 분의 시간이 소요될 것입니다. 테스트 코드는 빠르게 확인하고, 수정하고 반영하는 데에 큰 의미가 있기 때문에 속도가 느린 테스트는 테스트 코드의 의미 중 많은 부분을 잃어버린 것과 같다고 볼 수 있습니다.
* Independent/Isolated 각각의 테스트는 서로 독립적이며 서로 의존해서는 안 됩니다. 좋은 단위 테스트는 최소한의 단위의 테스트에 집중할 수 있게 각 테스트들이 서로에게 영향을 주어서는 안됩니다. 만약 다른 코드에 의존성이 높거나 영향을 많이 주고받고 있는 경우에는 완전히 통제된 상황에서 테스트를 진행하기 어려울 수 있으며 테스트가 실패하게 되었을 경우 그 원인이 불분명한 경우가 발생할 수 있습니다.
* Repeatable 테스트는 언제 어디서나 같은 결과가 반복되어야 합니다. 즉 모든 환경을 통제하여 매번 예상한 결과대로 테스트가 진행되게 해야 합니다. 이를 위해서 통제가 어려운 부분에 대해서는 테스트를 위한 객체를 만들어주는 방법을 선택하기도 합니다.
* Self-Validating 테스트는 Bool을 이용하여 성공/실패에 대해서 스스로 검증이 가능해야 합니다. 테스트 코드 내부에서 이 테스트가 잘 동작했는지를 판별할 수 있어야 합니다.
* Timely 이상적인 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현해야 합니다. 만약 실제 코드를 구현한 후에 테스트 코드를 작성할 경우 테스트하기가 매우 까다롭거나 불가능하도록 설계가 되어있을 지도 모릅니다
